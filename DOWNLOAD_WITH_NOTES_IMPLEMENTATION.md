# Download with Notes Feature Implementation

## Overview

This implementation adds a new "Download document + notes" feature to Paperless-ngx that allows users to download both the original document AND a separate text file containing all associated notes with their metadata, packaged together in a ZIP archive.

## Features

- **New API Endpoint**: `/api/documents/{id}/download_with_notes_files/`
- **Frontend Integration**: Added download options in the document detail view
- **ZIP Archive**: Downloads both the original document and a separate notes text file
- **Complete Note Information**: Includes note ID, creation date, creator username, and note content
- **Smart UI**: Button always shows in dropdown, regardless of document type

## Backend Implementation

### New Endpoint: `download_with_notes_files`

**Location**: `src/documents/views.py`

**Functionality**:
- Retrieves document with notes and user information
- Creates a ZIP archive containing:
  - The original document file
  - A separate text file with document metadata and notes
- Returns proper HTTP response with ZIP content type

**ZIP Archive Contents**:
1. **Original Document**: The actual document file (PDF, image, etc.)
2. **Notes File**: `{document_title}_notes.txt` containing:
   ```
   Document: [Document Title]
   Document ID: [ID]
   Created: [Creation Date]
   Added: [Added Date]
   Correspondent: [Correspondent Name] (if exists)
   Document Type: [Document Type] (if exists)
   Tags: [Tag1, Tag2, ...] (if exists)

   NOTES:
   ==================================================
   Note ID: [Note ID]
   Created: [Note Creation Date]
   Creator: [Username]
   Content: [Note Content]
   ------------------------------
   [Additional notes...]
   ==================================================
   ```

### API Documentation

Added OpenAPI schema documentation for the new endpoint:
```python
download_with_notes_files=extend_schema(
    description="Download both the original document and a separate notes file as a ZIP archive",
    responses={200: OpenApiTypes.BINARY},
),
```

## Frontend Implementation

### Document Service

**Location**: `src-ui/src/app/services/rest/document.service.ts`

**New Method**:
```typescript
getDownloadWithNotesFilesUrl(id: number): string {
  return this.getResourceUrl(id, 'download_with_notes_files')
}
```

### Document Detail Component

**Location**: `src-ui/src/app/components/document-detail/document-detail.component.ts`

**Updated Method**:
```typescript
downloadWithNotes() {
  // Downloads a ZIP file containing both the original document and notes
  // Includes proper error handling and mobile sharing support
}
```

### UI Integration

**Location**: `src-ui/src/app/components/document-detail/document-detail.component.html`

**Added UI Elements**:
1. **Download Dropdown**: Added "Download document + notes" option to the main download dropdown
2. **Actions Menu**: Added "Download document + notes" option to the Actions dropdown menu
3. **Always Visible**: The dropdown now shows regardless of document type (archive or original)

## Usage

### For Users

1. **Navigate to Document Detail View**: Open any document in the detail view
2. **Access Download Options**:
   - Click the download button dropdown arrow, or
   - Go to Actions menu → "Download document + notes"
3. **Download**: The system will generate and download a ZIP file containing:
   - The original document file
   - A text file with document metadata and all notes

### For Developers

**API Usage**:
```bash
GET /api/documents/{document_id}/download_with_notes_files/
```

**Response**: ZIP file (application/zip) containing both files

## Technical Details

### Security
- Uses existing permission system (`has_perms_owner_aware`)
- Requires `view_document` permission
- Follows same security model as other download endpoints

### Performance
- Efficient database queries with `select_related` and `prefetch_related`
- In-memory ZIP creation using `io.BytesIO`
- Proper file handling and cleanup

### Error Handling
- Graceful handling of missing documents
- Proper HTTP status codes (404, 403)
- Frontend error messages for user feedback

### File Naming
- ZIP file: `{title}_with_notes.zip`
- Notes file: `{title}_notes.txt`
- Original document: Preserves original filename
- Proper filename normalization for safe downloads

## Testing

The implementation includes:
- Python syntax validation
- TypeScript compilation verification
- Frontend build verification

## Compatibility

- **Backend**: Compatible with existing Django REST framework structure
- **Frontend**: Compatible with existing Angular component architecture
- **Database**: No schema changes required
- **API**: Follows existing API patterns and conventions

## Future Enhancements

Potential improvements that could be added:
1. **Format Options**: Support for different output formats (JSON, XML, etc.)
2. **Note Filtering**: Allow downloading only specific notes
3. **Custom Templates**: User-configurable output templates
4. **Bulk Download**: Support for downloading multiple documents with notes
5. **Note Attachments**: Include any note attachments in the download

## Files Modified

### Backend
- `src/documents/views.py`: Added `download_with_notes_files` endpoint and OpenAPI documentation

### Frontend
- `src-ui/src/app/services/rest/document.service.ts`: Added `getDownloadWithNotesFilesUrl` method
- `src-ui/src/app/components/document-detail/document-detail.component.ts`: Updated `downloadWithNotes` method
- `src-ui/src/app/components/document-detail/document-detail.component.html`: Updated UI elements

## Conclusion

This implementation provides a comprehensive solution for downloading documents with their associated notes as separate files in a ZIP archive, maintaining consistency with the existing codebase architecture and user experience patterns. The feature is ready for production use and follows all established conventions and security practices.