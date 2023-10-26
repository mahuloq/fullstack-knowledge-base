# To make own custom pipes make a new file with the format

'pipePurpose.pipe.ts'

# a pipe that shortens strings would for example look like this

import { Pipe, PipeTransform } from "@angular/core";

@Pipe({
name: "shorten",
})
export class ShortenPipe implements PipeTransform {
transform(value: any) {
if (value.length > 10) {
return value.substr(0, 10) + " ...";
}
return value;
}
}

# also need to import this into the app.module.ts

declarations: [AppComponent, ShortenPipe],

# You can add custom parameters to your pipe as follows

{{ server.name | shorten : 15 }}

import { Pipe, PipeTransform } from "@angular/core";

@Pipe({
name: "shorten",
})
export class ShortenPipe implements PipeTransform {
transform(value: any, limit: number) {
if (value.length > limit) {
return value.substr(0, limit) + " ...";
}
return value;
}
}
