import { ElementRef, type OnDestroy, type OnInit } from '@angular/core';
import type { TourAnchorDirective } from 'ngx-ui-tour-core';
import type { INgbStepOption } from './step-option.interface';
import * as i0 from "@angular/core";
import * as i1 from "@ng-bootstrap/ng-bootstrap";
export declare class TourAnchorNgBootstrapDirective implements OnInit, OnDestroy, TourAnchorDirective {
    tourAnchor: string;
    isActive: import("@angular/core").WritableSignal<boolean>;
    readonly element: ElementRef<any>;
    private readonly tourService;
    private readonly tourStepTemplate;
    private popoverDirective;
    constructor();
    ngOnInit(): void;
    ngOnDestroy(): void;
    showTourStep(step: INgbStepOption): Promise<void>;
    private setOffsetModifier;
    hideTourStep(): void;
    static ɵfac: i0.ɵɵFactoryDeclaration<TourAnchorNgBootstrapDirective, never>;
    static ɵdir: i0.ɵɵDirectiveDeclaration<TourAnchorNgBootstrapDirective, "[tourAnchor]", never, { "tourAnchor": { "alias": "tourAnchor"; "required": false; }; }, {}, never, never, true, [{ directive: typeof i1.NgbPopover; inputs: {}; outputs: {}; }]>;
}
