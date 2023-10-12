If we had some info in our component like

export class AppComponent {
// numbers = [1, 2, 3, 4, 5];
oddNumbers = [1, 3, 5];
evenNumbers = [2, 4];
onlyOdd = false;
value = 5;
}

we can access that info and only display some info depending on its value like

   <div [ngSwitch]="value">
        <p *ngSwitchCase="5">Value is 5</p>
        <p *ngSwitchCase="10">Value is 10</p>
        <p *ngSwitchCase="100">Value is 100</p>
        <p *ngSwitchDefault="">Value is Default</p>
      </div>
