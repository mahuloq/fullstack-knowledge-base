For this to work you need
import { FormsModule } from '@angular/forms';

in app.module.ts

So just put

<input type="text" class="form-control" [(ngModel)]="serverName" />

interacts in both directions
