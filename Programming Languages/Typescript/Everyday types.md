#### 1. The primitives:
- string
- number
- boolean
#### 2. Arrays
- number[]
- string[]
- using `T<U>` ex: `Array<number>`
#### 3. Any
```ts
let obj: any = { x: 0 };
```
#### 4. Functions
```ts
function greet(name: string) {
	console.log("Hello, " + name.toUpperCase() + "!!");
}

function getFavoriteNumber(): number {
	return 26;
}
```
#### 5. Object types
```ts
function printCoord(pt: { x: number; y: number }) {
	console.log("The coordinate's x value is " + pt.x);
	console.log("The coordinate's y value is " + pt.y);
}
printCoord({ x: 3, y: 7 });

// Optional properties
function printName(obj: { first: string; last?: string }) {
}
printName({ first: "Bob" });
printName({ first: "Alice", last: "Alisson" });
```
#### 6. Union types
```ts
function printId(id: number | string) {
	console.log("Your ID is: " + id);
}
// OK
printId(101);
printId("202");
// Error
printId({ myID: 22342 });
```
#### 7. Type alias
```ts
type Point = {
	x: number;
	y: number;
};
// Exactly the same as the earlier example
function printCoord(pt: Point) {
	console.log("The coordinate's x value is " + pt.x);
	console.log("The coordinate's y value is " + pt.y);
}
```

#### 8. Interface
```ts
interface Point {
	x: number;
	y: number;
}
function printCoord(pt: Point) {
	console.log("The coordinate's x value is " + pt.x);
	console.log("The coordinate's y value is " + pt.y);
}
printCoord({ x: 100, y: 100 });
```

#### 9. Type vs interface
the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable.

**Comparison 1:**
```ts
// Interface
interface Animal {
  name: string;
}  
interface Bear extends Animal {
  honey: boolean;
}  
const bear = getBear();
bear.name;
bear.honey;

// Type
type Animal = {
  name: string;
}  
type Bear = Animal & { 
  honey: boolean;
}  
const bear = getBear();
bear.name;
bear.honey;
```

**Comparison 2:**
```ts
// Interface
interface Window {
  title: string;
}  
interface Window {
  ts: TypeScriptAPI;
}  
const src = 'const a = "Hello World"';
window.ts.transpileModule(src, {});

// Type
type Window = {
  title: string;
}  
type Window = {
  ts: TypeScriptAPI;
}  
 // Error: Duplicate identifier 'Window'.
```