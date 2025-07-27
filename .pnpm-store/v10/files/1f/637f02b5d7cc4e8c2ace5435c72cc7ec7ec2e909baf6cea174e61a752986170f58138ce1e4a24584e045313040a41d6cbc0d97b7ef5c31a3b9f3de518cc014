import * as i0 from '@angular/core';
import { Injectable, signal, inject, ElementRef, Directive, Input, input, Component, ChangeDetectionStrategy, TemplateRef, ViewChild, ContentChild, NgModule } from '@angular/core';
import * as i1 from '@ng-bootstrap/ng-bootstrap';
import { NgbPopover } from '@ng-bootstrap/ng-bootstrap';
import { TourService, TourHotkeyListenerComponent, BaseTourProxyAnchor } from 'ngx-ui-tour-core';
import { firstValueFrom } from 'rxjs';

class NgbTourService extends TourService {
    static { this.ɵfac = i0.ɵɵngDeclareFactory({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: NgbTourService, deps: null, target: i0.ɵɵFactoryTarget.Injectable }); }
    static { this.ɵprov = i0.ɵɵngDeclareInjectable({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: NgbTourService, providedIn: 'root' }); }
}
i0.ɵɵngDeclareClassMetadata({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: NgbTourService, decorators: [{
            type: Injectable,
            args: [{
                    providedIn: 'root',
                }]
        }] });

class TourStepTemplateService {
    static { this.ɵfac = i0.ɵɵngDeclareFactory({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourStepTemplateService, deps: [], target: i0.ɵɵFactoryTarget.Injectable }); }
    static { this.ɵprov = i0.ɵɵngDeclareInjectable({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourStepTemplateService, providedIn: 'root' }); }
}
i0.ɵɵngDeclareClassMetadata({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourStepTemplateService, decorators: [{
            type: Injectable,
            args: [{
                    providedIn: 'root'
                }]
        }] });

class TourAnchorNgBootstrapDirective {
    constructor() {
        this.isActive = signal(false);
        this.element = inject(ElementRef);
        this.tourService = inject(NgbTourService);
        this.tourStepTemplate = inject(TourStepTemplateService);
        this.popoverDirective = inject(NgbPopover, { host: true });
        this.popoverDirective.autoClose = false;
        this.popoverDirective.triggers = '';
        // eslint-disable-next-line @typescript-eslint/no-empty-function
        this.popoverDirective.toggle = () => { };
    }
    ngOnInit() {
        this.tourService.register(this.tourAnchor, this);
    }
    ngOnDestroy() {
        this.tourService.unregister(this.tourAnchor);
    }
    // noinspection JSUnusedGlobalSymbols
    async showTourStep(step) {
        if (this.popoverDirective.isOpen()) {
            await firstValueFrom(this.popoverDirective.hidden);
        }
        this.isActive.set(true);
        this.popoverDirective.ngbPopover = this.tourStepTemplate.template;
        if (step.useLegacyTitle) {
            this.popoverDirective.popoverTitle = step.title;
        }
        this.popoverDirective.container = 'body';
        const popoverClass = step.popoverClass ?? '';
        this.popoverDirective.popoverClass = `tour-step ${popoverClass}`;
        this.popoverDirective.placement = (step.placement || 'auto')
            .replace('before', 'left').replace('after', 'right')
            .replace('below', 'bottom').replace('above', 'top');
        const offset = step.backdropConfig?.offset;
        if (offset) {
            this.popoverDirective.popperOptions = options => this.setOffsetModifier(options, offset);
        }
        this.popoverDirective.positionTarget = this.element.nativeElement;
        this.popoverDirective.open({ step });
    }
    setOffsetModifier(options, offset) {
        const offsetModifier = options.modifiers
            ?.find(modifier => modifier.name === 'offset' && modifier.options), arrowHeight = 10;
        if (offsetModifier) {
            offsetModifier.options['offset'] = [0, offset + arrowHeight];
        }
        return options;
    }
    // noinspection JSUnusedGlobalSymbols
    hideTourStep() {
        this.isActive.set(false);
        this.popoverDirective.close();
    }
    static { this.ɵfac = i0.ɵɵngDeclareFactory({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourAnchorNgBootstrapDirective, deps: [], target: i0.ɵɵFactoryTarget.Directive }); }
    static { this.ɵdir = i0.ɵɵngDeclareDirective({ minVersion: "14.0.0", version: "19.0.5", type: TourAnchorNgBootstrapDirective, isStandalone: true, selector: "[tourAnchor]", inputs: { tourAnchor: "tourAnchor" }, host: { properties: { "class.touranchor--is-active": "isActive()" } }, hostDirectives: [{ directive: i1.NgbPopover }], ngImport: i0 }); }
}
i0.ɵɵngDeclareClassMetadata({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourAnchorNgBootstrapDirective, decorators: [{
            type: Directive,
            args: [{
                    selector: '[tourAnchor]',
                    hostDirectives: [NgbPopover],
                    host: {
                        '[class.touranchor--is-active]': 'isActive()'
                    }
                }]
        }], ctorParameters: () => [], propDecorators: { tourAnchor: [{
                type: Input
            }] } });

class TourDefaultStepTemplateComponent {
    constructor() {
        this.step = input.required();
        this.tourService = inject(NgbTourService);
    }
    static { this.ɵfac = i0.ɵɵngDeclareFactory({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourDefaultStepTemplateComponent, deps: [], target: i0.ɵɵFactoryTarget.Component }); }
    static { this.ɵcmp = i0.ɵɵngDeclareComponent({ minVersion: "17.0.0", version: "19.0.5", type: TourDefaultStepTemplateComponent, isStandalone: true, selector: "tour-default-step-template", inputs: { step: { classPropertyName: "step", publicName: "step", isSignal: true, isRequired: true, transformFunction: null } }, ngImport: i0, template: "@let step = this.step();\r\n\r\n<div\r\n    [style.width]=\"step.stepDimensions?.width\"\r\n    [style.min-width]=\"step.stepDimensions?.minWidth\"\r\n    [style.max-width]=\"step.stepDimensions?.maxWidth\"\r\n    class=\"main-container\"\r\n>\r\n    @if (!step?.useLegacyTitle && step?.title) {\r\n        <div class=\"title-container\">\r\n            <h5>{{ step?.title }}</h5>\r\n            <button\r\n                type=\"button\"\r\n                class=\"btn-close\"\r\n                aria-label=\"Close\"\r\n                (click)=\"tourService.end()\"\r\n            ></button>\r\n        </div>\r\n    }\r\n    <p\r\n        class=\"card-text\"\r\n        [innerHTML]=\"step?.content\"\r\n    ></p>\r\n    <div\r\n        class=\"buttons\"\r\n        [class.no-progress]=\"!step.showProgress\"\r\n    >\r\n        <button\r\n            [disabled]=\"!tourService.hasPrev(step)\"\r\n            class=\"btn btn-sm btn-outline-secondary prev\"\r\n            (click)=\"tourService.prev()\"\r\n        >\r\n            <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"16\" height=\"16\" fill=\"currentColor\" viewBox=\"0 0 16 16\">\r\n                <path d=\"M11.354 1.646a.5.5 0 0 1 0 .708L5.707 8l5.647 5.646a.5.5 0 0 1-.708.708l-6-6a.5.5 0 0 1 0-.708l6-6a.5.5 0 0 1 .708 0z\"/>\r\n            </svg>\r\n            {{ step?.prevBtnTitle }}\r\n        </button>\r\n        @if (step.showProgress) {\r\n            <div class=\"progress\">{{ tourService.steps.indexOf(step) + 1 }} / {{ tourService.steps.length }}</div>\r\n        }\r\n        @if (tourService.hasNext(step) && !step.nextOnAnchorClick) {\r\n            <button\r\n                class=\"btn btn-sm btn-outline-primary next\"\r\n                (click)=\"tourService.next()\"\r\n            >\r\n                {{ step?.nextBtnTitle }}\r\n                <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"16\" height=\"16\" fill=\"currentColor\" viewBox=\"0 0 16 16\">\r\n                    <path d=\"M4.646 1.646a.5.5 0 0 1 .708 0l6 6a.5.5 0 0 1 0 .708l-6 6a.5.5 0 0 1-.708-.708L10.293 8 4.646 2.354a.5.5 0 0 1 0-.708z\"/>\r\n                </svg>\r\n            </button>\r\n        }\r\n        @if (!tourService.hasNext(step)) {\r\n            <button\r\n                class=\"btn btn-sm btn-outline-primary\"\r\n                (click)=\"tourService.end()\"\r\n            >\r\n                {{ step?.endBtnTitle }}\r\n            </button>\r\n        }\r\n    </div>\r\n</div>\r\n", styles: [".main-container{padding:.5rem 1rem .75rem}.title-container{display:flex;align-items:center;justify-content:space-between;margin-bottom:.5rem;gap:.25rem}.title-container h5{overflow:hidden;text-overflow:ellipsis;white-space:nowrap;margin-bottom:0;line-height:1.5}.buttons{display:grid;grid-template-columns:1fr auto 1fr;align-items:center;gap:8px}.buttons>*{max-width:fit-content}.buttons>*:last-child{justify-self:flex-end}.buttons .progress{font-size:12px;font-weight:700;color:#00000073;white-space:nowrap}.buttons.no-progress{grid-template-columns:1fr 1fr}.buttons .btn{display:flex;align-items:center;gap:.25rem}.buttons .btn.prev{padding-left:.25rem}.buttons .btn.next{padding-right:.25rem}\n"], changeDetection: i0.ChangeDetectionStrategy.OnPush }); }
}
i0.ɵɵngDeclareClassMetadata({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourDefaultStepTemplateComponent, decorators: [{
            type: Component,
            args: [{ selector: 'tour-default-step-template', imports: [], changeDetection: ChangeDetectionStrategy.OnPush, template: "@let step = this.step();\r\n\r\n<div\r\n    [style.width]=\"step.stepDimensions?.width\"\r\n    [style.min-width]=\"step.stepDimensions?.minWidth\"\r\n    [style.max-width]=\"step.stepDimensions?.maxWidth\"\r\n    class=\"main-container\"\r\n>\r\n    @if (!step?.useLegacyTitle && step?.title) {\r\n        <div class=\"title-container\">\r\n            <h5>{{ step?.title }}</h5>\r\n            <button\r\n                type=\"button\"\r\n                class=\"btn-close\"\r\n                aria-label=\"Close\"\r\n                (click)=\"tourService.end()\"\r\n            ></button>\r\n        </div>\r\n    }\r\n    <p\r\n        class=\"card-text\"\r\n        [innerHTML]=\"step?.content\"\r\n    ></p>\r\n    <div\r\n        class=\"buttons\"\r\n        [class.no-progress]=\"!step.showProgress\"\r\n    >\r\n        <button\r\n            [disabled]=\"!tourService.hasPrev(step)\"\r\n            class=\"btn btn-sm btn-outline-secondary prev\"\r\n            (click)=\"tourService.prev()\"\r\n        >\r\n            <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"16\" height=\"16\" fill=\"currentColor\" viewBox=\"0 0 16 16\">\r\n                <path d=\"M11.354 1.646a.5.5 0 0 1 0 .708L5.707 8l5.647 5.646a.5.5 0 0 1-.708.708l-6-6a.5.5 0 0 1 0-.708l6-6a.5.5 0 0 1 .708 0z\"/>\r\n            </svg>\r\n            {{ step?.prevBtnTitle }}\r\n        </button>\r\n        @if (step.showProgress) {\r\n            <div class=\"progress\">{{ tourService.steps.indexOf(step) + 1 }} / {{ tourService.steps.length }}</div>\r\n        }\r\n        @if (tourService.hasNext(step) && !step.nextOnAnchorClick) {\r\n            <button\r\n                class=\"btn btn-sm btn-outline-primary next\"\r\n                (click)=\"tourService.next()\"\r\n            >\r\n                {{ step?.nextBtnTitle }}\r\n                <svg xmlns=\"http://www.w3.org/2000/svg\" width=\"16\" height=\"16\" fill=\"currentColor\" viewBox=\"0 0 16 16\">\r\n                    <path d=\"M4.646 1.646a.5.5 0 0 1 .708 0l6 6a.5.5 0 0 1 0 .708l-6 6a.5.5 0 0 1-.708-.708L10.293 8 4.646 2.354a.5.5 0 0 1 0-.708z\"/>\r\n                </svg>\r\n            </button>\r\n        }\r\n        @if (!tourService.hasNext(step)) {\r\n            <button\r\n                class=\"btn btn-sm btn-outline-primary\"\r\n                (click)=\"tourService.end()\"\r\n            >\r\n                {{ step?.endBtnTitle }}\r\n            </button>\r\n        }\r\n    </div>\r\n</div>\r\n", styles: [".main-container{padding:.5rem 1rem .75rem}.title-container{display:flex;align-items:center;justify-content:space-between;margin-bottom:.5rem;gap:.25rem}.title-container h5{overflow:hidden;text-overflow:ellipsis;white-space:nowrap;margin-bottom:0;line-height:1.5}.buttons{display:grid;grid-template-columns:1fr auto 1fr;align-items:center;gap:8px}.buttons>*{max-width:fit-content}.buttons>*:last-child{justify-self:flex-end}.buttons .progress{font-size:12px;font-weight:700;color:#00000073;white-space:nowrap}.buttons.no-progress{grid-template-columns:1fr 1fr}.buttons .btn{display:flex;align-items:center;gap:.25rem}.buttons .btn.prev{padding-left:.25rem}.buttons .btn.next{padding-right:.25rem}\n"] }]
        }] });

class TourStepTemplateComponent extends TourHotkeyListenerComponent {
    constructor() {
        super(...arguments);
        this.tourStepTemplateService = inject(TourStepTemplateService);
        this.tourService = inject(NgbTourService);
    }
    ngAfterContentInit() {
        this.tourStepTemplateService.template =
            this.stepTemplate ||
                this.stepTemplateContent ||
                this.defaultTourStepTemplate;
    }
    static { this.ɵfac = i0.ɵɵngDeclareFactory({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourStepTemplateComponent, deps: null, target: i0.ɵɵFactoryTarget.Component }); }
    static { this.ɵcmp = i0.ɵɵngDeclareComponent({ minVersion: "14.0.0", version: "19.0.5", type: TourStepTemplateComponent, isStandalone: true, selector: "tour-step-template", inputs: { stepTemplate: "stepTemplate" }, queries: [{ propertyName: "stepTemplateContent", first: true, predicate: TemplateRef, descendants: true }], viewQueries: [{ propertyName: "defaultTourStepTemplate", first: true, predicate: ["tourStep"], descendants: true, read: TemplateRef, static: true }], usesInheritance: true, ngImport: i0, template: "<ng-template #tourStep let-step=\"step\">\r\n    <tour-default-step-template\r\n        [step]=\"step\"\r\n    />\r\n</ng-template>\r\n", styles: ["::ng-deep .tour-step .popover-body{padding:0}\n"], dependencies: [{ kind: "component", type: TourDefaultStepTemplateComponent, selector: "tour-default-step-template", inputs: ["step"] }], changeDetection: i0.ChangeDetectionStrategy.OnPush }); }
}
i0.ɵɵngDeclareClassMetadata({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourStepTemplateComponent, decorators: [{
            type: Component,
            args: [{ selector: 'tour-step-template', imports: [
                        TourDefaultStepTemplateComponent
                    ], changeDetection: ChangeDetectionStrategy.OnPush, template: "<ng-template #tourStep let-step=\"step\">\r\n    <tour-default-step-template\r\n        [step]=\"step\"\r\n    />\r\n</ng-template>\r\n", styles: ["::ng-deep .tour-step .popover-body{padding:0}\n"] }]
        }], propDecorators: { defaultTourStepTemplate: [{
                type: ViewChild,
                args: ['tourStep', { read: TemplateRef, static: true }]
            }], stepTemplate: [{
                type: Input
            }], stepTemplateContent: [{
                type: ContentChild,
                args: [TemplateRef]
            }] } });

class TourProxyAnchorComponent extends BaseTourProxyAnchor {
    constructor() {
        super(...arguments);
        // noinspection JSUnusedGlobalSymbols
        this.anchorDirective = inject(TourAnchorNgBootstrapDirective, {
            host: true
        });
    }
    static { this.ɵfac = i0.ɵɵngDeclareFactory({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourProxyAnchorComponent, deps: null, target: i0.ɵɵFactoryTarget.Component }); }
    static { this.ɵcmp = i0.ɵɵngDeclareComponent({ minVersion: "14.0.0", version: "19.0.5", type: TourProxyAnchorComponent, isStandalone: true, selector: "tour-proxy-anchor", inputs: { anchorEl: "anchorEl" }, usesInheritance: true, hostDirectives: [{ directive: TourAnchorNgBootstrapDirective, inputs: ["tourAnchor", "anchorId"] }], ngImport: i0, template: ``, isInline: true, changeDetection: i0.ChangeDetectionStrategy.OnPush }); }
}
i0.ɵɵngDeclareClassMetadata({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourProxyAnchorComponent, decorators: [{
            type: Component,
            args: [{
                    selector: 'tour-proxy-anchor',
                    template: ``,
                    changeDetection: ChangeDetectionStrategy.OnPush,
                    imports: [],
                    hostDirectives: [{
                            directive: TourAnchorNgBootstrapDirective,
                            inputs: ['tourAnchor: anchorId']
                        }]
                }]
        }], propDecorators: { anchorEl: [{
                type: Input,
                args: [{ required: true }]
            }] } });

const COMPONENTS = [TourAnchorNgBootstrapDirective, TourStepTemplateComponent, TourProxyAnchorComponent];
class TourNgBootstrapModule {
    static { this.ɵfac = i0.ɵɵngDeclareFactory({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourNgBootstrapModule, deps: [], target: i0.ɵɵFactoryTarget.NgModule }); }
    static { this.ɵmod = i0.ɵɵngDeclareNgModule({ minVersion: "14.0.0", version: "19.0.5", ngImport: i0, type: TourNgBootstrapModule, imports: [TourAnchorNgBootstrapDirective, TourStepTemplateComponent, TourProxyAnchorComponent], exports: [TourAnchorNgBootstrapDirective, TourStepTemplateComponent, TourProxyAnchorComponent] }); }
    static { this.ɵinj = i0.ɵɵngDeclareInjector({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourNgBootstrapModule }); }
}
i0.ɵɵngDeclareClassMetadata({ minVersion: "12.0.0", version: "19.0.5", ngImport: i0, type: TourNgBootstrapModule, decorators: [{
            type: NgModule,
            args: [{
                    imports: COMPONENTS,
                    exports: COMPONENTS
                }]
        }] });

/**
 * Generated bundle index. Do not edit.
 */

export { TourAnchorNgBootstrapDirective, TourNgBootstrapModule, TourProxyAnchorComponent, NgbTourService as TourService, TourStepTemplateComponent };
//# sourceMappingURL=ngx-ui-tour-ng-bootstrap.mjs.map
