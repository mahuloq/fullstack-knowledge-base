# app.component.html

<div class="radio" *ngFor="let gender of genders">
          <label>
            <input type="radio" name="gender" ngModel [value]="gender" />
            {{ gender }}
          </label>
</div>

# app.component.ts

genders = ["male", "female"];
