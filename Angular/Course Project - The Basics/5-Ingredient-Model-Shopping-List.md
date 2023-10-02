import { Component, OnInit } from '@angular/core';

@Component({
selector: 'app-shopping-list',
templateUrl: './shopping-list.component.html',
styleUrls: ['./shopping-list.component.css'],
})
export class ShoppingListComponent {
ingredients = [];

constructor() {}

ngOnInit() {}
}

Added an ingredients array, also added ngOnOnit becuase my files dont seem to start with it.

Edited shopping list a bit

<div class="row">
  <div class="col-xs-10">
    <app-shopping-edit></app-shopping-edit>
    <hr />
   <ul class="list-group">
    <a class="list-group-item" style="cursor: pointer;"></a>
   </ul>
  </div>
</div>

---

Made model for ingredients

export class Ingredient {
constructor(public name: string, public amount: number) {}
}

---

Export class of ingredient

export class ShoppingListComponent {
ingredients: Ingredient[] = [
new Ingredient('Apples', 5),
new Ingredient('Tomatoes', 5),
];

constructor() {}

ngOnInit() {}
}

<a
class="list-group-item"
style="cursor: pointer"
\*ngFor="let ingredient of ingredients" >
{{ ingredient.name }} ({{ ingredient.amount }})
</a>

---

Made buttons for editing. For some reason my buttons were not seperated by a bit like they were in the videos.

<div class="row">
  <div class="col-xs-12">
    <form>
      <div class="row">
        <div class="col-sm-5 form-group">
          <label for="name">Name</label>
          <input type="text" class="form-control" id="name" />
        </div>
        <div class="col-sm-2 form-group">
          <label for="amount">Amount</label>
          <input type="number" class="form-control" id="amount" />
        </div>
      </div>
      <div class="row">
        <div class="col-cs-12">
          <button class="btn btn-success" type="submit">Add</button>
          <button class="btn btn-danger" type="button">Delete</button>
          <button class="btn btn-primary" type="button">Clear</button>
        </div>
      </div>
    </form>
  </div>
</div>
