# Thisoe's TypeScript Note

_[<< Back to Thisoe's Note](./README.md)_

> ### Links:
>
> - [`tsconfig.json` Docs](https://www.typescriptlang.org/tsconfig/)
>
> 

# [Mosh's](https://youtu.be/d56mG7DezGs) Course

## Recommended `tsconfig` attrs:
  - `noEmitOnError: true,` (Do not emit compiled JS dist files if any errors were reported.)
  - `"removeComments": true,`
  - `"noUnusedLocals": true,` (Detect unused vars.)
  - `"noUnusedParameters": true,`
  - `"noImplicitReturns": true,` (Check all paths (e.g. `if`,`else`) in a function to ensure they return a value.)

## Built-in types
  - `any`
    - Default of uninitialized vars.
    - **DO NOT USE `any`.**
  - `enum`
      - E.g.
      ```ts
      const enum Size { Small = 1, Medium, Large}
      let mySize: Size = Size.Medium
      console.log(mySize)
      // 2
      ```
    
  - `unknown` [See here](#unknown)
  - `never` [See here](#never)
  - `tuple` [See here](#tuple)

## arrays
```ts
let nums: number[] = [1, 2, 3]

// Strict number of items
let use: [number, string] = [1, 'Thisoe']
```

## functions
```ts
function calcTax(income:number, taxYear = 2022):number {
  if(taxYear < 2022)
    return income*1.2
  return income*1.3
}

// Restrict 2 args
console.log( calcTax(10_0000,2023) )
```

## obj & `type`
```ts
type Employee = {
  readonly id:number,
  name:string,
  retire: (date:Date)=> void
}

let employee:Employee = {
  id: 1,
  name: 'Thisoe',
  retire:(date:Date)=>{
    console.log(date)
  }
}
```

Union types:
`let weight:number|string`
```ts
type Draggable = {
  drag: ()=>void
}

type Resizable = {
  resize: ()=>void
}

type UIWidget = Draggable & Resizable

let $txt:UIWidget = {
  drag: _=>{},
  resize: _=>{}
}
```

## optional operators

  1. Optional Chaining

  ```ts
  obj?.length
  ```

  2. Optional Element Access
  ```ts
  const arr: number[] | null = null
  const element = arr?.[0]
  ```

  3. Optional Call
  ```ts
  type User = {
    name?: string
    greet?: () => void
  }
  
  const user: User = {}
  user.greet?.()
  ```

# ...
