Unlike Structural directives
attribute directives dont add or remove elements, they only change the element they were placed on.

<p [ngStyle]="{ backgroundColor: getColor() }">
  {{ "Server" }} with ID {{ serverId }} is {{ getServerStatus() }}
</p>

serverStatus = 'offline';

constructor() {
this.serverStatus = Math.random() > 0.5 ? 'online' : 'offline';
}

getServerStatus() {
return this.serverStatus;
}
getColor() {
return this.serverStatus === 'online' ? 'green' : 'red';
}

Set server to default.
Then yse contructor to change it depending on output of Math.random.

getServerStatus method returns offline or online.
get color returns green or red depending on above value.

the ngStyle is bound to recieve the value and change background color.

Class Attribute

<p
  [ngStyle]="{ backgroundColor: getColor() }"
  [ngClass]="{ online: serverStatus === 'online' }"
>
  {{ "Server" }} with ID {{ serverId }} is {{ getServerStatus() }}
</p>

@Component({
selector: 'app-server',
templateUrl: './server.component.html',
styles: [
`
.online {
color: white;
}
`,
],
})
