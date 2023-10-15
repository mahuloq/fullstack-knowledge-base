  <li role="presentation" class="active" routerLink="/"><a>Home</a></li>
        <li role="presentation"><a routerLink="/servers">Servers</a></li>
        <li role="presentation"><a [routerLink]="['/users']">Users</a></li>

      Navigate by putting

      routerLink in the a element.

      You can also use binding for more advanced cases

be careful with paths as without / it becomes a relative link
so it tries to get to the path from the current path.

you can also navigate with relative ./

or go back with ../

You can assign classes when the Router Link is clicked with

routerLinkActive="class-here"

you can also include options with

[routerLinkActiveOptions]="{ javascript here, us exact:true to avoid home page problems }"
