forbiddenUsernames = ["Chris", "Anna"];

# if the code below doesnt find the name, it outputs -1, which is considered true, so we have to !== -1 to make it work properly.

forbiddenNames(control: FormControl): { [s: string]: boolean } {
if (this.forbiddenUsernames.indexOf(control.value) !== -1) {
return { nameisForbidden: true };
}
return null;
}
