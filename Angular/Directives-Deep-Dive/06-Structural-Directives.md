\*ngIf doesnt exist, what angular does is transform that into

<ng-template [ngIf]>
</ng-template>

We can make our own custom \* directive

import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

@Directive({
selector: '[appUnless]',
})
export class UnlessDirective {
@Input() set appUnless(condition: boolean) {
if (!condition) {
this.vcRef.createEmbeddedView(this.templateRef);
} else {
this.vcRef.clear();
}
}
constructor(
private templateRef: TemplateRef<any>,
private vcRef: ViewContainerRef
) {}
}

and we replaced

  <div *ngIf="!onlyOdd">
          <li
            class="list-group-item"
            [ngStyle]="{
              backgroundColor: even % 2 !== 0 ? 'yellow' : 'transparent'
            }"
            [ngClass]="{ odd: even % 2 !== 0 }"
            *ngFor="let even of evenNumbers"
          >
            {{ even }}
          </li>
        </div>

with

 <div *appUnless="onlyOdd">
          <li
            class="list-group-item"
            [ngClass]="{ odd: even % 2 !== 0 }"
            [ngStyle]="{
              backgroundColor: even % 2 !== 0 ? 'yellow' : 'transparent'
            }"
            *ngFor="let even of evenNumbers"
          >
            {{ even }}
          </li>
        </div>
