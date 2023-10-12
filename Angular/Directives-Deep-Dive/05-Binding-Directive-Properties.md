What you can do if you want to be able to change the colors from the outside, is have Inputs that are accessible through property binding.

@Input() defaultColor: string = 'transparent';
@Input() highlightColor: string = 'teal';

are the defualts, but on the html element, this would change the styling.

   <p appBasicHighlight>Style me with basic directives!</p>
      <p appBetterHighlight [defaultColor]="'orange'" [highlightColor]="'red'">
        Style me with basic directives!
 </p>

you can also do a bit of a different way

    <p appBasicHighlight>Style me with basic directives!</p>
      <p appBetterHighlight defaultColor="orange" highlightColor="red">
        Style me with basic directives!

 </p>

and get rid of the [] around them, but also have to get rid of '' of the inner declaration

import {
Directive,
ElementRef,
HostBinding,
HostListener,
OnInit,
Renderer2,
Input,
} from '@angular/core';

@Directive({
selector: '[appBetterHighlight]',
})
export class BetterHighlightDirective implements OnInit {
@Input() defaultColor: string = 'transparent';
@Input() highlightColor: string = 'teal';

@HostBinding('style.backgroundColor') backgroundColor: string = '';

constructor(private elRef: ElementRef, private renderer: Renderer2) {}

ngOnInit(): void {
// this.renderer.setStyle(
// this.elRef.nativeElement,
// 'background-color',
// 'teal'
// );

    this.backgroundColor = this.defaultColor;

}
@HostListener('mouseenter') mouseover(eventData: Event) {
// this.renderer.setStyle(
// this.elRef.nativeElement,
// 'background-color',
// 'teal'
// );
this.backgroundColor = this.highlightColor;
}

@HostListener('mouseleave') mouseleave(eventData: Event) {
// this.renderer.setStyle(
// this.elRef.nativeElement,
// 'background-color',
// 'transparent'
// );
this.backgroundColor = this.defaultColor;
}
}
