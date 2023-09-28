servers.component.ts
export class ServersComponent implements OnInit {
allowNewServer = false;

constructor() {
setTimeout(() => {
this.allowNewServer = true;
}, 2000);
}

ngOnInit() {}
}

then in servers.component.html
<button class="btn btn-primary" [disabled]="!allowNewServer">Add Server</button>
<app-server></app-server>
<app-server></app-server>

the [] around disabled let us attach it to a property
