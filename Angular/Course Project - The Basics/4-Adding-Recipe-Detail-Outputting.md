<div class="row">
  <div class="col-xs-12">
    <button class="btn btn-success">New Recipe</button>
  </div>
</div>
<div class="row">
  <div class="col-xs-12">
    <a href="#" 
    class="list-group-item clearfix" 
    *ngFor="let recipe of recipes">
      <div class="pull-left">
        <h4 class="list-group-item-heading">Recipe Name</h4>
        <p class="list-group-item-text">Description</p>
      </div>
      <span class="pull-right">
        <img src="" alt="" class="img-responsive" style="max-height: 50px" />
      </span>
    </a>
    <app-recipe-item></app-recipe-item>
  </div>
</div>

---

Then second video

<div class="row">
  <div class="col-xs-12">
    <button class="btn btn-success">New Recipe</button>
  </div>
</div>
<hr />
<div class="row">
  <div class="col-xs-12">
    <a href="#" class="list-group-item clearfix" *ngFor="let recipe of recipes">
      <div class="pull-left">
        <h4 class="list-group-item-heading">{{ recipe.name }}</h4>
        <p class="list-group-item-text">{{ recipe.description }}</p>
      </div>
      <span class="pull-right">
        <img
          src="{{ recipe.imagePath }}"
          alt="{{ recipe.name }}"
          class="img-responsive"
          style="max-height: 50px"
        />
      </span>
    </a>
    <app-recipe-item></app-recipe-item>
  </div>
</div>

My recipe seems to span the width of the page though, though it looks like it only happens at certain page width and looks correct on full size pages.

---

Worked on Recipe Detail Component

<div class="row">
  <div class="col-xs-12">
    <img src="" alt="" class="img-responsive" />
  </div>
</div>
<div class="row">
  <div class="col-xs-12">
    <h1>Recipe Name</h1>
  </div>
</div>
<div class="row">
  <div class="col-xs-12">
    <div class="btn-group">
      <button type="button" class="btn btn-primary dropdown-toggle">
        Manage Recipe <span class="caret"></span>
      </button>
      <ul class="dropdown-menu">
        <li><a href="#">Shoppint List</a></li>
        <li><a href="#">Edit Recipe</a></li>
        <li><a href="#">Delete Recipe</a></li>
      </ul>
    </div>
  </div>
</div>
<div class="row">
  <div class="col-xs-12">Description</div>
</div>
<div class="row"><div class="col-xs-12">Ingredients</div></div>
