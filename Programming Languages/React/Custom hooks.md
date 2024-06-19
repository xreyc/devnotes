Hooks are reusable functions.
When you have component logic that needs to be used by multiple components, we can extract that logic to a custom Hook.
Custom Hooks start with **"use"**. Example: `useFetch`.

#### Example 1: useCounter custom hook
useCounter.js
```jsx
import { useState } from 'react'

// Custom hook for counter functionality
function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue) // State to keep track of count

  // Function to increment count
  const increment = () => setCount(prevState => prevState + 1)

  // Returns count and increment function
  return [count, increment]
}
```
App.js

```jsx
import React from 'react';
import useCounter from './useCounter'

// Component using the useCounter Hook
function CounterComponent() {
  const [count, increment] = useCounter() // Utilizing useCounter

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  )
}
```

#### Example 2: data fetching hook
useFetch.js
```jsx
import { useState, useEffect } from 'react'

// Custom hook for fetching data
function useFetch(url) {

  const [data, setData] = useState(null) // State for data
  const [loading, setLoading] = useState(true) // State for loading
  const [error, setError] = useState(null) // State for error handling

  useEffect(() => {
    const fetchData = async () => {
      setLoading(true)
      setError(null)

      try {
        const response = await fetch(url)

        if (!response.ok) {
          throw new Error(`An error occurred: ${response.statusText}`)
        }

        const jsonData = await response.json()
        setData(jsonData)
      } catch (error) {
        setError(error.message)
      } finally {
        setLoading(false)
      }
    }

    fetchData()
  }, [url]) // Dependency array with url

  return { data, loading, error }
}
```
App.jsx
```jsx
import React from 'react'
import useFetch from './useFetch'

// Component using the useFetch Hook
function DataDisplayComponent({ url }) {
  const { data, loading, error } = useFetch(url) // Utilizing useFetch

  if (loading) return <p>Loading...</p>
  if (error) return <p>Error: {error}</p>

  return <div>{JSON.stringify(data, null, 2)}</div>
}
```

#### Example 3: Form
userForm.js
```jsx
import { useState } from 'react'

function useFormInput(initialValue) {
  const [value, setValue] = useState(initialValue)

  const handleChange = (e) => {
    setValue(e.target.value)
  }

  // Returns an object with value and onChange properties
  return {
    value,
    onChange: handleChange
  }
}
```

App.jsx
```jsx
import React from 'react'
import useFormInput from './useFormInput'

function FormComponent() {

  const name = useFormInput('')
  const age = useFormInput('')

  const handleSubmit = (e) => {
    e.preventDefault()
    console.log(`Name: ${name.value}, Age: ${age.value}`)
  }

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label>
          Name:
          {/* The spread operator here is equivalent to value={name.value} onChange={name.onChange} */}
          <input type="text" {...name} />
        </label>
      </div>
      <div>
        <label>
          Age:
          <input type="number" {...age} />
        </label>
      </div>
      <button type="submit">Submit</button>
    </form>
  )
}
```

#### Example 4: another counter
```jsx
import { useState } from 'react';

const useCounter = (initialValue = 0, step = 1) => {
  const [count, setCount] = useState(initialValue);

  const increment = () => {
    setCount(count + step);
  };

  const decrement = () => {
    setCount(count - step);
  };

  const reset = () => {
    setCount(initialValue);
  };

  return { count, increment, decrement, reset };
};

export default useCounter;

```

App.jsx
```jsx
import React from 'react';
import useCounter from './useCounter';

const CounterComponent = () => {
  const { count, increment, decrement, reset } = useCounter(0, 2);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
      <button onClick={decrement}>Decrement</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
};

export default CounterComponent;

```