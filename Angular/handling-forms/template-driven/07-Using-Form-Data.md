  <div class="row" *ngIf="submitted">
    <div class="col-xs-12">
      <h3>Your Data</h3>
      <p>Username: {{ user.username }}</p>
      <p>Mail: {{ user.email }}</p>
      <p>Secret Question: Your first {{ user.secretQuestion }}</p>
      <p>Answer:{{ user.answer }}</p>
      <p>Gender:{{ user.gender }}</p>
    </div>
  </div>

submitted = false;

onSubmit() {
this.submitted = true;
this.user.username = this.signupForm.value.userData.username;
this.user.email = this.signupForm.value.userData.email;
this.user.secretQuestion = this.signupForm.value.secret;
this.user.answer = this.signupForm.value.questionAnswer;
this.user.gender = this.signupForm.value.gender;

this.signupForm.reset()
}
