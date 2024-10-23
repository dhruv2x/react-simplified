# React-Simplified

### History

- **2011**: React was developed by Jordan Walke, a software engineer at Facebook, as a JavaScript library.
- **2013**: React was open-sourced by Facebook at JSConf US, introducing it to the public.
- **2015**: React Native was introduced, allowing developers to build mobile applications using React for iOS and Android.
- **2016**: React 15 was released, improving performance and introducing the concept of "error boundaries."
- **2017**: React 16 (codenamed "Fiber") was released, bringing a complete rewrite of the React core to improve rendering and support for error boundaries and fragments.
- **2020**: React 17 was released with a focus on gradual upgrades, allowing multiple React versions on the same page.
- **2021**: React 18 was announced, with features like concurrent rendering and automatic batching.

### Basics

[https://www.codewithharry.com/tutorial/react-home/](https://www.codewithharry.com/tutorial/react-home/)

**Coding in JSX**

Earlier we had to make an HTML element or append it into existing ones with methods like `createElement()` / `appendChild()`

```jsx
const elem = React.createElement('h1', {}, 'Hello World!');
```

Now we can just do it directly, like this:

`const elem = <h1>Hello World!</h1>`

React commnets

```jsx
Outside JSX
//
inside JSX
      {/*Step 2 create provider*/}
```

**Component Constructor**

Constructor gets called when the component is initiated. This is where you initiate the component's properties. In React we have states which update on page without reload. Constructor properties are kept in state.

We also need to add `super()` statement, which executes the parent component's constructor and component gets access to all the functions of the parent component, like this:

```jsx
class Cat extends React.Component {
  constructor() {
    super();
    this.state = { color: "orange" };
  }
  render() {
    return <h1>Meow's color is {this.state.color}</h1>;
  }
}
```

```jsx
const obj = { name: 'John' };
obj.name = 'Doe'; // This is allowed because we are mutating the object
// But reassigning the entire object will cause an error:
obj = { name: 'Jane' }; // Error! Assignment to constant variable

```

hello world

```jsx
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<h1>Hello, world!</h1>);
```

Basic Increment Program

```cpp
import { useState } from "react";

function App() {
  const [val,setVal]=useState(0);
  const increaseVal=()=>{
    setVal(val+1);
  }
  const decreaseVal=()=>{
    setVal(val-1);
  }
  return (
    <>
    <p>Increment Project</p>
    <h1>Value is {val}</h1>
    <button onClick={increaseVal}>increase</button>
    <br/>
    <br/>
    <button onClick={decreaseVal}>Decrease</button>
    </>
  );
}

export default App;

```

Note

```jsx
  const increaseVal=()=>{
    console.log("start : "+val);
    setVal(val+1);
    
    console.log("after val+1 : "+val);
    setVal(val+1);
    
    console.log("after val+2 : "+val);
    setVal(val+1);
  }
```

here output will be same as react treat each setVal as same beacause we are performing same operation

if we do setVal(val+1) and setVal(val+2) then it will pick last setVal(val+2), it will pick final state update.

### React Fiber

The goal of React Fiber is to increase its suitability for areas like animation, layout, and gestures. Its headline feature is **incremental rendering**: the ability to split rendering work into chunks and spread it out over multiple frames. Other key features include the ability to pause, abort, or reuse work as new updates come in; the ability to assign priority to different types of updates; and new concurrency primitives.

*reconciliation*

The algorithm React uses to diff one tree with another to determine which parts need to be changed.

*update*

A change in the data used to render a React app. Usually the result of `setState`. Eventually results in a re-render.

Reconciliation is the algorithm behind what is popularly understood as the "virtual DOM.”

Scenario:

Let’s say you have a list of items in a React app, and you want to update one item in the list when a user clicks a button.

**Before Update:**

You have a list in your app’s DOM:

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>

```

Now, the user clicks a button to change "Item 2" to "Updated Item 2."

---

**Virtual DOM**:

When the state changes, React first updates the **virtual DOM**, not the real DOM.

1. **Old Virtual DOM**:
    
    ```html
    <ul>
      <li>Item 1</li>
      <li>Item 2</li>
      <li>Item 3</li>
    </ul>
    
    ```
    
2. **New Virtual DOM** (after state update):
    
    ```html
    <ul>
      <li>Item 1</li>
      <li>Updated Item 2</li>
      <li>Item 3</li>
    </ul>
    
    ```
    

### **Reconciliation**:

- React now compares (diffs) the **old virtual DOM** with the **new virtual DOM**.
- It finds that only one change occurred: **"Item 2" was updated**.
- Using the **reconciliation** process, React decides that only this part of the real DOM needs to be updated. It doesn't re-render the entire list, only modifies **Item 2**.

**After Reconciliation**:

- React updates the real DOM efficiently:
    
    ```html
    <ul>
      <li>Item 1</li>
      <li>Updated Item 2</li>
      <li>Item 3</li>
    </ul>
    
    ```
    

- The **Virtual DOM** was used to create a lightweight version of the actual DOM.
- The **Reconciliation** process compared the old and new virtual DOMs, and React efficiently updated only the necessary part of the real DOM.

The reconciler does the work of computing which parts of a tree have changed; the renderer then uses that information to actually update the rendered app.

goal of Fiber is to enable React to take advantage of scheduling

React Destructuring

Instead of accessing `props` using `props.name`, destructuring allows you to pull out specific props directly:

```jsx
function Greeting({ name, age }) {
  return (
    <div>
      Hello, {name}. You are {age} years old.
    </div>
  );
}
```

if you want to pass js object then directly pass that to other component

```
function App() {
  var json={
    name:"dhruv",
    package:9
  }
  return (
    <div>
      <PageC data={json}/>
    </div>
  )
}
```

```jsx
and then access it

function PageC({data}) {
  return (
    <div>Heloow {data.package}</div>
  )
}
```

Change colour based on button clicking mini project

```cpp
function App() {
  const changeColor=(name)=>{
    setCol(name);
  }
  let [col,setCol]=useState("white");
  return (
    <div className={`bg-${col} d-flex justify-content-center flex-wrap gap-2 mt-3`}>
    <Button variant="primary"onClick={() => changeColor("primary")} >Primary</Button>
    <Button variant="secondary" onClick={() => changeColor("secondary")}>Secondary</Button>
    <Button variant="success" onClick={() => changeColor("success")}>Success</Button>
   
  </div>
  );
}

export default App;

```

learnings

1. if you have function and you want to pass some data to it use call back function when calling it.

```jsx
const changeColor=(name)=>{
    setCol(name);
  }
  
  use onClick={()=>changeColor("primary")}
  
  instead of
  
  
  use onClick={changeColor("primary")}
  
  bcz onCLick needs function not just a return value of function
```

1. if you want to use variables in className use ``

```cpp
  <div className={`bg-${col} d-flex justify-content-center flex-wrap gap-2 mt-3`}>
```

### React Component lifecycle

1. mounting - render, componentDidMount
2. updating - rener, compponentDidUpdate
3. unmounting - componentWillUnmount

### API calls

The `useEffect` hook should be placed at the top level inside the `App` component, not inside a function that is triggered by a button click.

when we need to call api by any event link button clicking then do not use useEffect just simply use fetch

most api calls return values as string so need to convert into json

```cpp
const fetchCountries = async () => {
    setLoading(true);
    try {
      const response = await fetch('https://restcountries.com/v3.1/all');
      const data = await response.json();// convert rsponse into json
      const countryNames = data.map(country => country.name.common); //now start look using .map and pick name key and inside another key called common and create list of country names
      setCountries(countryNames);
    } catch (error) {
      console.error('Error fetching country data:', error);
    }
    setLoading(false);
  };
```

Now if we just want to directly call function without need to clicking any button then use useEffect with empty dependency like below

```cpp
 useEffect(() => {
    const fetchCountries = async () => {
      try {
        const response = await fetch('https://restcountries.com/v3.1/all');
        const data = await response.json();
        const countryNames = data.map((country) => country.name.common);
        setCountries(countryNames);
        console.log(countryNames);
        countries.map((country, index) => (console.log("index is"+index)));
      } catch (error) {
        console.error('Error fetching country data:', error);
      }
      setLoading(false);
    };

    fetchCountries(); // Fetch countries on component mount
  }, []); // Empty dependency array means this will run only once when the component mounts
```

```cpp
import React, { useState, useEffect } from 'react';

const CountryList = () => {
  const [countries, setCountries] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const fetchCountries = async () => {
      try {
        const response = await fetch('https://restcountries.com/v3.1/all');
        const data = await response.json();
        const countryNames = data.map((country) => country.name.common);
        setCountries(countryNames);
      } catch (error) {
        console.error('Error fetching country data:', error);
      }
      setLoading(false);
    };

    fetchCountries(); // Fetch countries on component mount
  }, []); // Empty dependency array means this will run only once when the component mounts

  return (
    <div>
      {loading ? <p>Loading...</p> : null}
      <ul>
        {countries.map((country, index) => (
          <li key={index}>{country}</li>
        ))}
      </ul>
    </div>
  );
};

export default CountryList;

```

 from array of countries we can use like below in rendering as we need to give index as well

```cpp
  {countries.map((country, index) => (            
          <li key={index}>{country}</li>
        ))}
```

POST method

```jsx
const data = await fetch(
  "http://localhost:8000/mad-over-meme/v1/api/room/create",
  {
    method: "POST",
    headers: {
      "Content-Type": "application/json", // Make sure you set the headers
    },
    body: JSON.stringify(body),
  }
);
const jsondata = await data.json();
const APImsg = jsondata.message;
setmsg(APImsg);
```

### Routers

Here’s imp things to keep in mind

1. if project contains redirection from one page to another then we must add routes
2. create seperate routes file and defile routes using createBrowserRouter

```jsx
import React from 'react'
import { createBrowserRouter } from 'react-router-dom';
import Test from './Test';
import App from './App';
const router=  createBrowserRouter(
   [
    {
      path: '/',
      element: <App/>   
  },
    {
        path: 'test',
        element: <Test/>   
    },
  ]);

export default router;
```

1. wrap <app/> with <RouterProvider router={router}>

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import { RouterProvider } from 'react-router-dom';
import App from './App';
import router from './router';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <RouterProvider router={router}>
    <App />
  </RouterProvider>
);
```

1. multiple ways we can do navigation

i. using useNavigate

ii. using Link

```jsx
import React from 'react'
import { Link, useNavigate } from 'react-router-dom';
function App() {
  
  const navigator=useNavigate();
  function increaseCounter(){  
  navigator('/test');    
  }
  
  return (
    <>
	    //using navigator
     <button onClick={increaseCounter}>test page navigation</button>
     //using Link
     <Link to="/test">Go to test page</Link>
    </>
  )
}

export default App
```

Project:  create 2 page and using url we can redirect

```cpp
export default function App() {
  return (
    <>
   <Routes>
        <Route path='/'Component={First}/>
        <Route path='sec'Component={Second}/>
   </Routes>
    </>
  );
}

also wrap app with BrowserRouter

 <BrowserRouter>
    <App/>
 </BrowserRouter>
```

```cpp
<Route path="*" Component={NotFound} /> {/* Handle non-existing routes */}

<Route path="/Contact/*" element={<Home />} />  {/* Handle roytes after fixed text routes */}
```

Now if user wants to navigate between pages we can use Link componenet

```cpp
 <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
      <Link to="/contact">Contact</Link>
    </nav>
```

get the url of window

```cpp
function MyComponent() {
  const currentUrl = window.location.href;

  return (
    <div>
      <p>Current URL: {currentUrl}</p>
    </div>
  );
}

```

Create nested routes, if you want to keep home content as it is and change other content based on routes use Outlet and createBrowserRouter 

Note : do not use wrap index.js in BrowserRouter if you are using RouterProvider as we can’t use router inside router 

```jsx
import { createBrowserRouter } from 'react-router-dom';
import App from './App';
import About from './About';
const router=createBrowserRouter([
    {
        path:"/",
        element:<App/>,
        children:[
            {
                path:"/about",
                element:<About/>
            }
        ]
    },
    
]);
export default router;

and App.js

import React from 'react'
import { Link, Outlet, useNavigate } from 'react-router-dom'

function App() {
    const navigator=useNavigate();
    const showAbout=()=>{
        navigator("/about");
    }
  return (
    <div>
        <Link to="/about">About Us</Link>
        <p>Hi</p> 
        <Outlet/>
    </div>
  )
}

export default App
```

Outlet will show content based on what user click button, url will be changed based on routes

we can also use below way. it works same!

```cpp
export default function App() {
  return (
    <>
      <Router>
        <Routes>
          <Route path="/" element={<Home />}>
            {/* Define nested routes here */}
            <Route path="contact" element={<Contact />} />
            <Route path="NotFound" element={<NotFound />} />
          </Route>
        </Routes>
      </Router>
    </>
  );
}

```

Pass parameter in url and access that in page

```cpp
export default function App() {
  return (
    <>
      <Router>
        <Routes>
          <Route path="/" element={<Home />}>
            {/* Define nested routes here */}
            <Route path="contact/:userid" element={<Contact />} />
            <Route path="contact" element={<Contact />} />
            <Route path="NotFound" element={<NotFound />} />
          </Route>
        </Routes>
      </Router>
    </>
  );
}

```

we can access userid in contact page using useParams function.

```cpp
import React from 'react'
import { useParams } from 'react-router-dom'
function Contact() {
  const {userid} =useParams();
  return (
    <div>this is Second pagevand id is {userid}</div>
  )
}

export default Contact
```

### Loaders

Loaders allow you to fetch data **before rendering** a route. ensuring the data is ready when the component is mounted. This can be considered a more optimized and declarative approach to fetching data compared to manual `useEffect` hooks inside components.

```cpp
import React from "react";
import Home from "./components/Home";
import Contact, { githubInfoLoader }  from "./components/Contact";
import NotFound from "./components/NotFound";
import {
  Route,
  Routes,createBrowserRouter,RouterProvider,
  BrowserRouter as Router,
} from "react-router-dom";

export default function App() {

  // Define routes with loaders
const router = createBrowserRouter([
  {
    path: "/",
    element: <Home />,
    children: [
      {
        path: "contact",
        element: <Contact />,
        loader: githubInfoLoader,  // Attach the loader here
      },
      {
        path: "*",
        element: <NotFound />,
      },
    ],
  },
]);
  return <RouterProvider router={router} />;
}

```

```cpp
import React, { useEffect, useState } from 'react'
import { useLoaderData } from 'react-router-dom'
function Contact() {
  // const [data,setData]=useState([]);
  // useEffect(()=>{
  //   fetch('https://api.github.com/users/hiteshchoudhary').then(res=>res.json()).then(data=>setData(data))
  //   },[])
  const data = useLoaderData();
  return (
    <div>followers is {data.followers}</div>
  )
}

export default Contact;

export const githubInfoLoader = async () => {
  const response = await fetch('https://api.github.com/users/hiteshchoudhary')
  return response.json()
}
```

### Context API

In React, **props drilling** refers to the process of passing data from a parent component to deeply nested child components through multiple intermediate components, even if those intermediate components don't need the data themselves. This can make the code harder to manage and maintain as the app grows. To avoid props drilling, you can use context or state management libraries like Redux.

```cpp
import React from 'react';

function App() {
  const Parent = () => {
    return (
      <div>
        Parent
        <Child data="20LPA" />
      </div>
    );
  };

  const Child = (props) => {
    return (
      <h1>
        Inside Child
        <GrandChild data={props.data} />
      </h1>
    );
  };

  const GrandChild = (props) => {
    return (
      <h1>
        Inside Grandchild, value is {props.data}
      </h1>
    );
  };

  return (
    <>
      <Parent />
    </>
  );
}

export default App;

```

Solve above issue using context API

```cpp
import React, { createContext, useContext } from 'react';

// 1. Create a Context
const DataContext = createContext();

function App() {
  // 2. Provide the Context value
  return (
    <DataContext.Provider value="20LPA">
      <Parent />
    </DataContext.Provider>
  );
}

const Parent = () => {
  return (
    <div>
      Parent
      <Child />
    </div>
  );
};

const Child = () => {
  return (
    <h1>
      Inside Child
      <GrandChild />
    </h1>
  );
};

const GrandChild = () => {
  // 3. Consume the Context value using useContext hook
  const data = useContext(DataContext);

  return <h1>Inside Grandchild, value is {data}</h1>;
};

export default App;

```

Or we may use sperate files for context relates stuff!

```cpp
import React, { createContext, useContext } from 'react';

import { useData, DataContext, DataProvider } from './HelloContext/DataProvider';  // Import the custom hook to access the context

function App() {
  return (
    <DataProvider>
      <Parent />
    </DataProvider>
  );
}

const Parent = () => {
  return (
    <div>
      Parent
      <Child />
    </div>
  );
};

const Child = () => {
  return (
    <h1>
      Inside Child
      <GrandChild />
    </h1>
  );
};

const GrandChild = () => {
  const data = useData();

  return <h1>Inside Grandchild, value is {data}</h1>;
};

export default App;

```

separate file

```cpp
// DataContext.js
import React, { createContext, useContext } from 'react';

// Create the Context
export const DataContext = createContext();

// Create a Provider component
export const DataProvider = ({ children }) => {
  const value = "20LPA"; // This is the shared value

  return (
    <DataContext.Provider value={value}>
      {children}
    </DataContext.Provider>
  );
};

// Custom hook to use the DataContext
export const useData = () => {
  return useContext(DataContext);
};

```

- **Spread Operator: → mostly for array concatination**

`const languages = ['JS', 'Python', 'Java'];
const morelanguages = ['C', 'C++', 'C#']

const allLanguages = [...languages, ...morelanguages]`

["JS","Python","Java","C","C++","C#"]

Strict Mode enables the following development-only behaviors:

- Your components will [re-render an extra time](https://react.dev/reference/react/StrictMode#fixing-bugs-found-by-double-rendering-in-development) to find bugs caused by impure rendering.
- Your components will [re-run Effects an extra time](https://react.dev/reference/react/StrictMode#fixing-bugs-found-by-re-running-effects-in-development) to find bugs caused by missing Effect cleanup.
- Your components will [be checked for usage of deprecated APIs.](https://react.dev/reference/react/StrictMode#fixing-deprecation-warnings-enabled-by-strict-mode)

Handle Multiple Inputs

```jsx
import { useState } from 'react';

function Form() {
  const [data, setData] = useState({});

  const handleChange = (e)=>{
    setData({...data, [e.target.name]: e.target.value})
  }

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Your email is: ${data.email} and your name is: ${data.name}`)
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Enter your email: <input type="email" name='email' value={data.email} onChange={handleChange} />
      </label>
      <label>
        Enter your name: <input type="text" name='name' value={data.name} onChange={handleChange} />
      </label>
      <input type="submit" />
    </form>
  )
}

export default Form;
```

## Styling react componenet

We can style using 3 ways

1. within componenet

```jsx
 const h1Style = {
    backgroundColor: 'purple',
    color: 'white'
  }

  return (
    <>
      <h1 style={h1Style}>CodeWithHarry</h1>
    </>
  );
```

1. use local css file for that componenet 

naming shold be like this FILENAME.module.csss

```jsx
import styles from './index.module.css'; 

const Home = () => {
    return (
        <button className={styles.button}>Click me!</button>
    )
};

export default Home;
```

1. use global css file

```jsx
import  './index.css'; 

const Home = () => {
    return (
        <button className='button'>Click me!</button>
    )
};

export default Home;
```

## Hooks info

### memo

What memo does is, it just monitors if `props` have changed, if they have it re-renders, if they haven't it doesn't render again.

`props` is an object and javascript is very fast in comparing objects as it doesn't compare the whole object, it just checks the address!

```jsx
export default memo(Navbar);
```

### UseEffect and useRef

Automatic counter - useEffect demo

```jsx
import { useEffect, useState } from 'react';
import  './form.css'
function Form() {

 let [counter,setCounter]=useState(0);
 
 useEffect(()=>{
  setTimeout(()=>{
    setCounter(counter+1);
  },1000);  
 })
 
  return (
   <>
      <p className='test'>I havae rendered {counter}</p>
    </>
  )
}

export default Form;
```

Random Password generator mini project - useEffect demo

```cpp
import React, { useState , useCallback ,useEffect} from 'react'

function App() {
  //f=declare variables
  
  const [pin,setPin]=useState('');
  const [pinLength,setpinLength]=useState(5);
  const [NumberAllowed,isNumberAllowed]=useState(false);
  const [SpecialCharAllowed,isSpecialCharAllowed]=useState(false);

  const generatePin=useCallback(()=>{
    let str="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz";
    let newpin="";
    if(NumberAllowed)
      str+="0123456789";
    if(SpecialCharAllowed)
      str+="!@#$%^&*-_+=[]{}~";

    for(let i=1;i<=pinLength;i++){
      let ind=Math.floor(Math.random()*str.length+1);
      newpin+=str.charAt(ind);
    }
    setPin(newpin);
  },[pinLength,NumberAllowed,SpecialCharAllowed]);

  useEffect(() => {
    generatePin()
  }, [pinLength,NumberAllowed,SpecialCharAllowed])
  
  return (
    <>
    <div className='m-3'>
    <h1 className='m-3'>Password Generator</h1>
    <p>generated pass is {pin}</p>
    <p>length is {pinLength}</p>
    <br/>
    <input type='text'value={pinLength} onChange={(e) => {setpinLength(e.target.value)}}></input>
    <button onClick={generatePin}>Enter length</button>
    <br/>
    <input type='checkbox'   checked={NumberAllowed} onChange={() => {
              isNumberAllowed(prev => !prev);
          }}></input> 
    <label >Numbers</label>
    <br/>
    <input type='checkbox' checked={SpecialCharAllowed}   onChange={() => {
              isSpecialCharAllowed(prev => !prev);
          }}></input> 
    <label>Special Characters</label>
    </div>
    </>
  )
}

export default App
```

learnings

1. if we want to execute some function if state variable changes then use useEffect

```cpp
useEffect(() => {
    generatePin()
  }, [pinLength,NumberAllowed,SpecialCharAllowed])
```

1. we can get the latest changed value of input text using e.target.value

```cpp
 onChange={(e) => {setpinLength(e.target.value)}}
```

1. if want to cache calculated value then use useCallback, it returns memoized callback function. caching a value so that it does not need to be recalculated. One reason to use `useCallback` is to prevent a component from re-rendering unless its props have changed.
2. we can copy text using below line

```cpp
 window.navigator.clipboard.writeText(password)
```

1. we can add extra effects using useRef

d**esn't cause re-render**

```cpp
declare

  const passwordRef=useRef(null);
  
assign this ref to any input field that you want to highlight

	 ref={passwordRef}
	 
use in onclick function

	 passwordRef.current?.select();
   
```

```jsx
import { useRef } from "react";
import ReactDOM from "react-dom/client";

function App() {
  const inputElement = useRef();

  const focusInput = () => {
    inputElement.current.focus();
  };

  return (
    <>
      <input type="text" ref={inputElement} />
      <button onClick={focusInput}>Focus Input</button>
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

### **useContext**

 `useContext` helps to manage states globally, i.e. between components. 

### useReducer

similar to useState

write custom state logic

```jsx
import { useEffect, useReducer, useState } from 'react';
import  './form.css'
function Form() {
    
    const reducer=(state,action)=>{
        if(action.type==="plus"){
            return state+1;
        }
        else{
            return state-1;
        }
    }
    const [counter,dispatch]=useReducer(reducer,0);

  return (
   <>
      <p>Counter using useReducer {counter}</p>
      <button onClick={()=>dispatch({type:"plus"})}>increment</button>
      <button onClick={()=>dispatch({type:"minus"})}>Decremenet</button>

    </>
  )
}

export default Form;
```

### **React useCallback and useMemo**

React `useCallback` Hook returns a memoized callback function.

It is done so that it does not need to be recalculated resulting in improved performance.

If we don't use useCallback function would run on every render

for example if we have 2 componenet

parent and child

if parent re-render child also re-renders

useCallback → memoized functiom

useMemo → memoized value

```jsx
import React, { useState, useCallback, memo } from 'react';

// Child component that accepts a prop 'onClick'
const Child=memo(({ onClick })=> {
  console.log("Child rendered");
  return <button onClick={onClick}>Click me</button>;
});

function Parent() {
  const [count, setCount] = useState(0);

  // Memoizing the handleClick function
  const handleClick = useCallback(() => {
    console.log("Button clicked");
  }, []); // Dependencies array is empty, so it won't change

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment Count</button>
      <Child onClick={handleClick} /> {/* Passing the memoized function */}
    </div>
  );
}

export default Parent;

```

**Lazy Loading**:

- Lazy loading is a performance optimization technique that defers the loading of a component until it's actually needed, reducing the initial load time for the application.
- In React, lazy loading is achieved using `React.lazy()` and `Suspense`. `React.lazy()` allows you to load a component dynamically, while `Suspense` is used to display a fallback UI (like a spinner) until the component finishes loading.

```jsx
const LazyComponent = React.lazy(() => import('./LazyComponent'));

function App() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}

```

### useHistory - similar to useNavigator

- `useHistory` is a hook from React Router that allows you to programmatically manipulate the browser’s history stack. This is useful when you need to navigate users around the app without using links.
- Common methods:
    - `history.push("/path")`: Navigates to a new route and adds it to the history stack.
    - `history.replace("/path")`: Replaces the current route with a new one without adding a new entry in the history stack.
    - `history.goBack()`: Goes back to the previous page.

```jsx
import { useHistory } from "react-router-dom";

function Navigation() {
  const history = useHistory();

  const goToHome = () => {
    history.push("/home");
  };

  return <button onClick={goToHome}>Go to Home</button>;
}

```

### **Higher-Order Components (HOC):**

**What is a Higher-Order Component (HOC)?**

- An HOC is a function that takes a component as input and returns a new enhanced component with added functionality. HOCs allow code reuse by abstracting shared logic between components.
- Syntax:
    
    ```jsx
    jsx
    Copy code
    const withEnhancement = (WrappedComponent) => {
      return class EnhancedComponent extends React.Component {
        render() {
          return <WrappedComponent {...this.props} />;
        }
      };
    };
    
    ```
    

**Example**:

- dImagine you want to add authentication logic to multiple components. Instead of repeating the same logic, you can create an HOC that wraps each component and handles the authentication check.
    
    ```jsx
    
    const withAuth = (Component) => {
      return function AuthenticatedComponent(props) {
        if (!props.isAuthenticated) {
          return <Redirect to="/login" />;
        }
        return <Component {...props} />;
      };
    };
    
    const Dashboard = (props) => <div>Welcome to the Dashboard!</div>;
    export default withAuth(Dashboard);
    
    ```
    

**Use Cases of HOCs**:

1. Authorization: HOCs can be used to restrict access to certain components based on the user’s authentication status.

# Redux

1. **Store**: The centralized state container that holds the entire app's state. It allows state to be accessed, updated, and subscribed to through Redux's mechanisms.
2. **Slice**: A portion of the Redux state managed by a single reducer, typically created using `createSlice`. Each slice handles actions and state logic for a specific part of the state.
3. **Reducer**: A pure function that determines how the state changes in response to an action. It's responsible for returning the new state based on the previous state and the action dispatched.
    
    single reducer contains multiple functions which methods which picked based on action name
    
4. **Action**: An object that describes an intention to change the state. It has a `type` field and optionally a payload that provides the necessary data for the state update.
5. **Dispatch**: The method used to send an action to the Redux store, triggering the appropriate reducer to handle the action and update the state.
6. **useSelector**: A hook provided by Redux to access a specific part of the state from the store inside a React component. It efficiently selects the desired data from the Redux store.

### Simple counter app using redux

1. create store inside redux folder and name store.js 

```jsx
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from '../features/counter/counterSlice'
const store = configureStore({
 
});
export default store;

```

1. wrap App with <Provider store={store}>
2. crate slices

```jsx
import { createSlice } from '@reduxjs/toolkit'

const initialState = {
  value: 0,
}

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload
    },
  },
})

// Action creators are generated for each case reducer function
export const { increment, decrement, incrementByAmount } = counterSlice.actions

export default counterSlice.reducer
```

1. import that slice in store and add reducer

```jsx
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from '../features/counter/counterSlice'
const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});
export default store;

```

1. use data and send actions via dispatch

```jsx
import React from 'react'
import PageA from './pages/PageA'
import { useDispatch, useSelector } from 'react-redux'
import { decrement, increment } from '../src/features/counter/counterSlice'
function App() {
  const count=useSelector((state)=>state.counter.value)
  const dispatch=useDispatch();
  return (
    <div>
      <PageA/>
      <div>
        <button
          aria-label="Increment value"
          onClick={() => dispatch(increment())}
        >
          Increment
        </button>
        <span>{count}</span>
        <button
          aria-label="Decrement value"
          onClick={() => dispatch(decrement())}
        >
          Decrement
        </button>
      </div>
    </div>
  )
}

export default App;
```

### What if you just want some static data to be accessible to your entire project

1. create  slice

```jsx
import { createSlice } from '@reduxjs/toolkit'

const initialState = {
  name:"dhruv",
  package:9
}

export const staticDataSlice = createSlice({
  name: 'staticData',
  initialState,
  reducers: {
    
  }
})

export default staticDataSlice.reducer
```

1. attach it with store

```jsx
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from '../features/counter/counterSlice'
import  dummyReducer  from '../features/counter/staticDataSlice';
const store = configureStore({
  reducer: {
    counter: counterReducer,
    staticData: dummyReducer
  },
});
export default store;

```

1. use anywhere

```jsx
import React from 'react'
import { useSelector } from 'react-redux'

function PageC() {
const data=useSelector((state)=>state.staticData);
    return (
    <div>Hi my package is {data.package}</div>
  )
}

export default PageC
```

### createAsyncThunk

 utility provided by Redux Toolkit to handle asynchronous operations, like fetching data from an API, in a clean and standardized way.

It allows you to define an asynchronous function (often a promise) and automatically generates actions for the three possible states: **pending**, **fulfilled**, and **rejected**.
