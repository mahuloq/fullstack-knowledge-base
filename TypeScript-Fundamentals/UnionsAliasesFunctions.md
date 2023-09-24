# Union-Type-Aliases-Function-Types

Unions allow you to declare more than one type as being accepted for a set of data. Seperate the types with the | symbol.

Type-Alias - type VaruableNameHere = { name: string; age: number };

then you can sub VaruableNameHere for that in the future

Functions and Types - Will infer types within a function by setting some numbers

like

function add(a: number, b: number) {
return a + b;
}

or

function add(a: number, b: number): number | string {
return a + b;
}
