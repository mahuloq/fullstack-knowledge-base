## You can allow more parametes programmatically with

    this.router.navigate(["/servers", id, "edit"], {
      queryParams: { allowEdit: "1" },
      fragment: "loading",
    });

## or inline with

<a
[routerLink]="['/servers', 5, 'edit']"
[queryParams]="{ allowEdit: '1' }"
[fragment]="'loading'"
href="#"
class="list-group-item"
\*ngFor="let server of servers" >
{{ server.name }}
</a>

## Can get that data with

console.log(this.route.snapshot.queryParams);
console.log(this.route.snapshot.fragment);

    this.route.queryParams.subscribe();
    this.route.fragment.subscribe();
