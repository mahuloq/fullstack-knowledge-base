## Can use ngModelGroup="groupname" to group the data from the object. Can also #userData="ngModelGroup" to use it for ngIf

 <div id="user-data" ngModelGroup="userData" #userData="ngModelGroup">
          <div class="form-group">
            <label for="username">Username</label>
            <input
              ngModel
              name="username"
              type="text"
              id="username"
              class="form-control"
              required
            />
          </div>
          <button class="btn btn-default" type="button">
            Suggest an Username
          </button>
          <div class="form-group">
            <label for="email">Mail</label>
            <input
              ngModel
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
          </div>
        </div>
        <p *ngIf="!userData.valid && userData.touched">User Data is Invalid!</p>
