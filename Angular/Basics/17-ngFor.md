servers = ['TestServer', 'TestServer2'];

this.servers.push(this.serverName);

<app-server \*ngFor="let server of servers"></app-server>
