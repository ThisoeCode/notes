# Thisoe's TypeScript Note

[<< Back to Thisoe's Note](./README.md)

`tsconfig.json` [Official Docs](https://www.typescriptlang.org/tsconfig/)


# [Mosh](https://youtu.be/d56mG7DezGs)'s Course

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
function calcTax(income: number): number{

}
```



    
