# setup form in ts file

ngOnInit(): void {
this.signupForm = new FormGroup({
username: new FormControl(null),
email: new FormControl(null),
gender: new FormControl("male"),
});

# to link your reactive form to the html form you need to type

<form [formGroup]="signupForm">

# which tells the form, not to make its own, but to follow your information. Then on the inputs you put

formControlName="nameOfThingHere"

# add the following to get access to the data

<form [formGroup]="signupForm" (ngSubmit)="onSubmit()">

# then within the .ts file

onSubmit() {
console.log(this.signupForm);
}
