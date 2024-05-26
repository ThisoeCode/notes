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
  - `tuple` [See here](#type-tuple)

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


# [WDS's](https://www.youtube.com/playlist?list=PLZlA0Gpn_vH_z2fqIg50_POJrUkJgBu7g) Course

## Generics
1. Generic functions
```ts
function getFirstElement<ElementType>(array: ElementType[]){
  return array[0]
}

const nums = [1,2,3]
const firstNum = getFirstElement(nums) // " type: number "

const strs = ['a','b']
const firstNum = getFirstElement(strs) // " type: string "
```

```ts
const map = new Map<string, number>()
map.set('a',1) // " type: string, number "

const map = new Map([['c',3]]) // " type: string, number "
map.set('a',1)

const map = new Map<string, Map<number,string>>()
  // " map: <string, Map<number,string>> "
```

2. Generic Types
```ts
type ApiResponse<Data> = {
  data: Data
  isError: boolean
}

// pass in generic here
const res:ApiResponse<{name:string, age:number}> = {
  data: {
    name: "Thisoe",
    age: 28,
  },
  isError: false,
}
```

  - Make allies type:
  ```ts
  type UserRes = ApiResponse<{name:string, age:number}>
  type BlogRes = ApiResponse<{title:string, content:string}>
  const res2:BlogRes = {
    data: {title: "Thisoe", content: ""},
    isError: false,
  }
  ```

  - Default generic
  ```ts
  type ApiResponse<Data={name:string}> = {
    data: Data
    err: boolean
  }

  const res:ApiResponse<number> = {
    data: 200,
    isError: false,
  }
  ```

  - Adheration (extensions & default)
  ```ts
  type ApiResponse<Data extends object = {name:string}> = {
    data: Data
    err: boolean
  }

  type StatusRes = {status: number}
  const res:StatusRes = {
    data: {status: 200},
    isError: false,
  }
  ```


# [Net Ninja's](https://www.youtube.com/playlist?list=PL4cUxeGkcC9gUgr39Q_yD6v-bSyMwKPUI) Course

## Type `tuple`
> // TODO Study https://youtu.be/tHSstkiVbc8



# Other Notes

## Other built-in types
(Tutorial: [Andrew Burgess](https://youtu.be/kWmUNChlzVw))

### `unknown`
All possible types are accepted.
```ts
let val:unknown = 1

if (typeof val === 'number') val++
if (typeof val === 'string') val.toUpperCase()
if (Array.isArray(val)) val.map(val)
if (
  val &&
  typeof cal === 'object' &&
  'foobar' in val &&
  typeof val.foobar === 'number'
) val.foobar = 2
```

### `never`
There is no possible type to sign to type `never`.
```ts
type A = number & string
// TS: `A:never`
```
```ts
type User = 'standard'|'admin'|'superadmin'

function login(user:User){
  switch(user){
    case 'standard': return true
    case 'admin': return true
    // case 'useradmin': return true
    default: // This will give a type error: `useradmin` cannot be `never`
      const _unreachable:never = user
      throw 'wrong user type'
  }
}
```

## Utility Types
### `Record<Keys, Type>`
(Tutorial: [Tim Mousk](https://youtu.be/d7EsXK_vBDQ))
```ts
type Statuses = 'err'|'suc'

// TS will check if the keys are in `Statuses` type
const obj:Record<Statuses, string> = {
  err: '',
  suc: '',
}
```




