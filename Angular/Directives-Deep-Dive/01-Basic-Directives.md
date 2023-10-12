Directives start with file name
.directive.ts

Then you make a class

export class BasicHighlightDirective{
}

then make a selector

@Directive({
selector: '[appBasicHighlight]',
})

and import needed info

import { Directive, ElementRef, OnInit } from '@angular/core';

example of working directive

import { Directive, ElementRef, OnInit } from '@angular/core';

@Directive({
selector: '[appBasicHighlight]',
})
export class BasicHighlightDirective implements OnInit {
constructor(private elementRef: ElementRef) {}

ngOnInit() {
this.elementRef.nativeElement.style.backgroundColor = 'green';
}
}
