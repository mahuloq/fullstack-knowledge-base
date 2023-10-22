# can bind ngModel to some value to set the defualt, also have to setup the value in the TS file. One Way binding

              <input
              [ngModel]="defaultQuestion"
              name="email"
              type="email"
              id="email"
              class="form-control"
              required
              email
              #email="ngModel"
            />
            <span *ngIf="!email.valid && email.touched"
              >Please enter a valid email!</span
            >

# Can also do two way binding to access it instantly

<div class="form-group">
          <textarea
            name="questionAnswer"
            rows="3"
            class="form-control"
            [(ngModel)]="answer"
          ></textarea>
        </div>
        <p>Your reply: {{ answer }}</p>

# once again setting a default valute in .ts
