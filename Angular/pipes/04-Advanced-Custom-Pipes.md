<input type="text" [(ngModel)]="filteredStatus" name="" id="" />

# Put this on your html to filter content.

import { Pipe, PipeTransform } from "@angular/core";

@Pipe({
name: "filter",
})
export class FilterPipe implements PipeTransform {
transform(value: any, filterString: string, propName: string): any {
if (value.length === 0 || filterString === "") {
return value;
}
const resultArray = [];
for (const item of value) {
if (item[propName] === filterString) {
resultArray.push(item);
}
}
return resultArray;
}
}

# this will filter the page, but if you added a server while in filter mode, it would not show up, you can force it to show up by entering the following

import { Pipe, PipeTransform } from "@angular/core";

@Pipe({
name: "filter",
pure: false,
})
export class FilterPipe implements PipeTransform {
transform(value: any, filterString: string, propName: string): any {
if (value.length === 0 || filterString === "") {
return value;
}
const resultArray = [];
for (const item of value) {
if (item[propName] === filterString) {
resultArray.push(item);
}
}
return resultArray;
}
}

# be careful as this can cause performance issues.
