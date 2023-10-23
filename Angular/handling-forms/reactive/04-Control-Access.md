 <div class="form-group">
          <label for="email">email</label>
          <input
            type="text"
            formControlName="email"
            id="email"
            class="form-control"
          />
          <span
            *ngIf="
              !signupForm.get('email').valid && signupForm.get('email').touched
            "
            class="help-block"
            >Please enter a valid email.</span
          >
        </div>

# can still use css

input.ng-invalid.ng-touched {
border: 1px solid red;
}

---

# You can create form groups as follows

ngOnInit(): void {
this.signupForm = new FormGroup({
userData: new FormGroup({
username: new FormControl(null, Validators.required),
email: new FormControl(null, [Validators.required, Validators.email]),
}),
gender: new FormControl("male"),
});
}

# to access the data, that is now nested you need to encase the elements in a div.

  <div formGroupName="userData">formstuffhere </div>
  
 # Then within that div, change the get to as follows

<span
\*ngIf="
!signupForm.get('userData.username').valid &&
signupForm.get('userData.username').touched
"
class="help-block" >Please enter a valid username.</span
            >
