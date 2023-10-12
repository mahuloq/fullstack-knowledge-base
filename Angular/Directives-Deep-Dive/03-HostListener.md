Can you Host Listener like an ElementListener to affect how the directive works.

import {
Directive,
ElementRef,
HostListener,
OnInit,
Renderer2,
} from '@angular/core';

@Directive({
selector: '[appBetterHighlight]',
})
export class BetterHighlightDirective implements OnInit {
constructor(private elRef: ElementRef, private renderer: Renderer2) {}

ngOnInit(): void {
// this.renderer.setStyle(
// this.elRef.nativeElement,
// 'background-color',
// 'teal'
// );
}
@HostListener('mouseenter') mouseover(eventData: Event) {
this.renderer.setStyle(
this.elRef.nativeElement,
'background-color',
'teal'
);
}

@HostListener('mouseleave') mouseleave(eventData: Event) {
this.renderer.setStyle(
this.elRef.nativeElement,
'background-color',
'transparent'
);
}
}
