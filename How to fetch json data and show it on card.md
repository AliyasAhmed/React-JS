```jsx
import React, { useEffect, useRef, useState } from 'react'

const App = () => {
  const [cards, setcards] = useState([])


  const jsondata = async()=>{
    let a = await fetch('https://jsonplaceholder.typicode.com/posts')
    let data = await a.json()
    setcards(data)
  }
  useEffect(()=>{
    jsondata()
  },[])
  return (
    <>
    <div>
      <div className="container">
      {cards.map((card)=>{
        return <div key={card.id} className="card">
          <h1>{card.title}</h1>
          <p>{card.body}</p>
          <span>{card.userId}</span>
        </div>
      })}
      </div>
    </div>
    </>
  )
}

export default App
```
