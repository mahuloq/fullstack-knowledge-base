<span
*ngIf="
!signupForm.get('userData.username').valid &&
signupForm.get('userData.username').touched
"
class="help-block" >
<span
*ngIf="
signupForm.get('userData.username').errors['nameisForbidden']
" >This Name is Forbidden</span
              >
<span
\*ngIf="signupForm.get('userData.username').errors['required']" >This field is required.</span
              >
</span>
