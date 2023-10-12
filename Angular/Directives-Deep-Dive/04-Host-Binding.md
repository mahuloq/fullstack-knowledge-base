Another way instead of Host Listener, is Host Binding

import {
Directive,
ElementRef,
HostBinding,
HostListener,
OnInit,
Renderer2,
} from '@angular/core';

@Directive({
selector: '[appBetterHighlight]',
})
export class BetterHighlightDirective implements OnInit {
@HostBinding('style.backgroundColor') backgroundColor: string = 'transparent';

constructor(private elRef: ElementRef, private renderer: Renderer2) {}

ngOnInit(): void {}

@HostListener('mouseenter') mouseover(eventData: Event) {

    this.backgroundColor = 'teal';

}

@HostListener('mouseleave') mouseleave(eventData: Event) {

    this.backgroundColor = 'transparent';

}
}
