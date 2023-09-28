Directives are Instructions in the DOM

<p appTurnGreen>Receives a green background</p>

@Directive({
selector:'[appTurnGreen]'
})
export class TurnGreenDirective{
...
}

\*ngIf=""

This works by turning on or off a component depending on if the value in ngIf is true or false.

ngIf Else

<p *ngIf="serverCreated; else noServer">
  Server was created, server name is {{ serverName }}
</p>

<ng-template #noServer><p>No server was created.</p></ng-template>

outpouts the #noServer data if the linked statement is false.
