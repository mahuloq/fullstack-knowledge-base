Can export class ServerComponent {
serverId = 10;
serverStatus = 'offline';

getServerStatus() {
return this.serverStatus;
}
}

then use it in the HTML

<p>{{ "Server" }} with ID {{ serverId }} is {{ getServerStatus() }}</p>
