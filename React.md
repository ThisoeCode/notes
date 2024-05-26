# Thisoe's React Note

_[<< Back to Thisoe's Note](./README.md)_

<!-- 
> ### Links:
>
> - 
>
> 
-->

# [Mosh's](https://youtu.be/SqcY0GlETPk) Course

## "key" prop
```ts
const items = ['a','b','c']

return <>
  <h1>List</h1>
  <ul>
    {items.map((item)=>(
      // REQUIRE A `KEY` PROPERTY
      <li>{item}</li>
    )}
  </ul>
</>
```

Give list items a unique key so that React can track each of the items.
```ts
<li key={item /* item.id */ }>{item}</li>
```

## Type Annotation
(_Some TypeScript stuff_)
```ts
export default function ListGroup(){
  const items = ['a','b','c']

  const handleClick = e=>console.log(e)
  // TS: `Parameter 'e' implicitly has an 'any' type.`

  return <>
    <ul>
      {items.map((item,i)=>{
        return <li key={i} onClick={handleClick}></li>
      })}
    </ul>
  </>
}
```
To fix this TS warning, we should add
```ts
import {MouseEvent} from "react"
// ...
const handleClick = (e:MouseEvent)=>console.log(e)
```

## `useState` hook
```ts
import {useStare} from 'react'

export default function ListGroup(){
  const items = ['a','b','c']
  const [selectedindex,setSelectedIndex] = useState(-1)

  return <>
    <ul>
      {items.map((item,index)=>{
        return <li
          key={i}
          onClick={_=>{setSelectedIndex(index)}}
        ></li>
      })}
    </ul>
  </>
}
```



