# Import Validators

ngOnInit(): void {
this.signupForm = new FormGroup({
username: new FormControl(null, Validators.required),
email: new FormControl(null, [Validators.required, Validators.email]),
gender: new FormControl("male"),
});
}

# can take an array of them
