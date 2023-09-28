You can create a method
onCreateServer() {
this.serverCreationStatus = 'The Server Was Created';
}

then call it by
<button
class="btn btn-primary"
(click)="onCreateServer()"
[disabled]="!allowNewServer"

>

the () contain the trigger or listen event
then execute the method.

Passing data

<label for="">Server Name</label>
<input type="text" class="form-control" (input)="onUpdateServerName($event)" />

the $event only works in the "" of an event binding, and represents the data from that event

serverName = '';

onUpdateServerName(event: any) {
this.serverName = (<HTMLInputElement>event.target).value;
}

<p>{{ serverName }}</p>

this sets a blank servername, then the onUpdate method captures it, and changes the value of serverName to the input entered
