email: new FormControl(
null,
[Validators.required, Validators.email],
this.forbiddenEmails

forbiddenEmails(control: FormControl): Promise<any> | Observable<any> {
const promise = new Promise<any>((resolve, reject) => {
setTimeout(() => {
if (control.value === "test@test.com") {
resolve({ emailIsForbidden: true });
} else {
resolve(null);
}
}, 1500);
});
return promise;
}
}
