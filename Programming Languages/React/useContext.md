React Context is a way to manage state globally.
It can be used together with the `useState` Hook to share state between deeply nested components more easily than with `useState` alone.
#### Create a user context
```jsx
import { useState, createContext } from "react";
import ReactDOM from "react-dom/client";

const UserContext = createContext()

function UserContextProvider({children}) {
  const [user, setUser] = useState("Jesse Hall");

  return (
    <UserContext.Provider value={user}>
      {children}
    </UserContext.Provider>
  );
}
```
#### Provider the user context on the app
```jsx
import { useState } from "react";
import Todos from "./components/Todos";

import UserContextProvider from "./UserContextProvider";

function App() {
  const [count, setCount] = useState(0);
  const [todos, setTodos] = useState(["todo 1", "todo 2"]);
  
  const updateTodos = () => {
    setTodos(["Mark1", "Mark2"]);
  }

  return (
    <UserContextProvider>
      <div>{count}</div>
      <Todos todos={todos} />
      <button onClick={() => { setCount(prev => prev + 1) }}>Increment</button>
      <button onClick={() => { updateTodos() }}>Update Todo</button>
    </UserContextProvider>
  )
}

export default App
```

#### Accessing the context
```jsx
function Component5() {
  const user = useContext(UserContext);

  return (
    <>
      <h1>Component 5</h1>
      <h2>{`Hello ${user} again!`}</h2>
    </>
  );
}
```