# Make sure FormsModule is imported into app.module.ts

# You can make angular recognize the form by putting

# ngModel name="" on the Inputs

# To get access to the data from ngForm

# <form (ngSubmit)="onSubmit(f)" #f="ngForm">

# onSubmit(form: NgForm) {

    console.log(form);

}

# This puts the data into an ngForm, you can access the value from there.

# Another way to acess the data is

@ViewChild("f") signupForm: NgForm;

onSubmit() {
console.log(this.signupForm);
}

# This will give you the same info, but allow you to access it before the submit button is hit

---
