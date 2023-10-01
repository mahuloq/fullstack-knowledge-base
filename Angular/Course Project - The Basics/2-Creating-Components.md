Create components manually

Create folder with component name
create "component name here".component.ts folder
and "component name here".component.html

within component.ts folder

import { Component } from '@angular/core';

@Component({
selector: 'app-"component name here"',
templateUrl: './"component name here".component.html',
})
export class HeaderComponent {}

Did some linking of components together and basic layout.
