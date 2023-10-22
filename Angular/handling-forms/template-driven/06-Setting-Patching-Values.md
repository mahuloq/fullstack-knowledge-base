suggestUserName() {
const suggestedName = "SuperUser";

# this way works, but it sets all of the form to set values, and you have to give every value.

    this.signupForm.setValue({
    //   userData: {
    //     username: suggestedName,
    //     email: "",
    //   },
    //   secret: "pet",
    //   questionAnswer: "",
    //   gender: "male",
    // });

# This way only modifies what you but in the patch value, note that this can only modify the form set with ngForm

# <form (ngSubmit)="onSubmit()" #f="ngForm">

# in the TS

# @ViewChild("f") signupForm: NgForm;

    this.signupForm.form.patchValue({
      userData: {
        username: suggestedName,
      },
    });

}
