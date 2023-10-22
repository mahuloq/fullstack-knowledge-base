# Validating Input

# <input

              ngModel
              name="email"
              type="email"
              id="email"
              class="form-control"
              required
              email
            />

# You can add required to the input, where the form will be considered invalid unless it is filled, the form module can also take certain other keywords as well, like email will make it so the input will be considered invalid unless it follows basic email behavior.

# if you check out the element selector, you will see that classes get added as you mess with the inputs, we can use that to code validation techniques into our program.

# we can put [disabled]="!f.valid"> on the button to disable it unless the form is valid. A simple way to CSS style that is

input.ng-invalid.ng-touched {
border: 1px solid red;
}

You can access the information within an element using binding

<span class="help-block" \*ngIf="!email.valid && email.touched" >Please enter a valid email!</span
