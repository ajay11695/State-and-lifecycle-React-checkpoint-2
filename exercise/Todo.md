# Explain the topics below in your own words. You can use diagrams, or you can also explain with code

1. What are the different ways to update state. Give example for each.

-  While a React component can have initial state, the real power is in updating its state — after all, if we didn't need to update the state, the component
shouldn't have any state. State is only reserved for data that changes in our component and is visible in the UI.
	```js
	// src/components/ClickityClick.js
import React from "react";
class ClickityClick extends React.Component { constructor() { super();

// Define the initial state:
this.state = {
  hasBeenClicked: false,
};
}

handleClick = () => { // Update our state here... };

render() { return (

  <div>
    <p>I have {this.state.hasBeenClicked ? null : "not"} been clicked!</p>
    <button onClick={this.handleClick}>Click me!</button>
  </div>
);
} }

export default ClickityClick;

// src/index.js import React from "react"; import ReactDOM from "react-dom";

import ClickityClick from "./components/ClickityClick";

ReactDOM.render(<ClickityClick />, document.getElementById("root"));

```
Instead of directly modifying the state using this.state, we use this.setState(). This is a function available to all React components that use state, and allows us to let React know that the component state has changed. This way the component knows it should re-render, because its state has changed and its UI will most likely also change. Using a setter function like this is very performant. While other frameworks like Angular.js use "dirty checking" (continuously checking for changes in an object) to see if a property has changed, React already knows because we use a built-in function to let it know what changes we'd like to make!

2. What are the different lifecycle methods in React. Give an use cases for each one of them.

- The mounting phase refers to the phase during which a component is created and inserted to the DOM.

The following methods are called in order.

- constructor() The constructor() is the very first method called as the component is “brought to life.”

The constructor method is called before the component is mounted to the DOM. In most cases, you would initialize state and bind event handlers methods within the constructor method.

Here’s a quick example of the constructor() React lifecycle method in action:

```jsx
const MyComponent extends React.Component {
  constructor(props) {
   super(props) 
    this.state = {
       points: 0
    }  
    this.handlePoints = this.handlePoints.bind(this) 
    }   
}
```
- static getDerivedStateFromProps() static getDerivedStateFromProps is a new React lifecycle method as of React 17 designed to replace componentWillReceiveProps.

Its main function is to ensure that the state and props are in sync for when it’s required.

The basic structure of the static getDerivedStateFromProps() looks like this:

```jsx
const MyComponent extends React.Component {
  ... 

  static getDerivedStateFromProps() {
//do stuff here
  }  
}
static getDerivedStateFromProps() takes in props and state:

... 

  static getDerivedStateFromProps(props, state) {
//do stuff here
  }  
  ```
  ```jsx 
   static getDerivedStateFromProps(props, state) { 
     return {
        points: 200 // update state with this
     }
  }  

  ...
Or you can return null to make no updates:

... 

  static getDerivedStateFromProps(props, state) {
    return null
  }  
  ```
  - ....... Why exactly is this lifecycle method important? While static getDerivedStateFromProps() is a rarely used lifecycle method, it comes in handy in certain scenarios.

Remember, this method is called (or invoked) before the component is rendered to the DOM on initial mount.

Here’s a quick example so you can see the static getDerivedStateFromProps() method in action. Consider a simple component that renders the number of points scored by a football team. As you may expect, the number of points is stored in the component state object:

```jsx
class App extends Component {
  state = {
    points: 10
  }

  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            You've scored {this.state.points} points.
          </p>
        </header>
      </div>
    );
  }
  ```

3. What is the difference between client side routing and server side routing.

- There are several differences between server-side routing and client-side routing and we are going to know all about them but first, we need to understand how the both of them work in there own unique way.
In server-side routing what usually happens when you are entering a URL for the first time or you want to change the page, maybe you click on the about us section or the navbar, the browser immediately detects that change in the URL then the browser makes an HTTP request to the server then the server re-renders the HTML into the application, now this can be very expensive and would require time-based on the internet speed and some other factors.

- In client side routing we don't need to go through all these stages, although when we first load the application that is inputing the web address the full react app is being rendered from the server, but after that when you want to change pages, maybe you click on the navbar the browser watches for change in the URL and immediately it detects change in the URL it uses the HTML5 history API to fetch the page that has already been loaded in when the application was first loaded in and returns it to the browser, and how react routerknows which particular page the user is making reference to is by going off to the set of configuration which would have a couple of URLs and components that would render to the root of those URLs, so when we click on the navbar react router goes on to search for the URL and its matching component and then that component is being rendered with a javascript function call.
So using react-router this would enable us to rerender our application with client-side javascript that is going to allow us to create a single page application that would enable us to swap out application simulating the page change.

- The difference between this two routing have been stated above server sides needs to keep making requests to the server in order for the application to rerender, but client side does not need to keep make request to the server, it just does it once when the application is being loaded into the browser any other navigation or page change is just being rendered from the already saved application, so a client side application can still function without the internet as long as it has already being loaded in with the internet.

4. Can you pass data from children to parent component using props. Explain your answer.

- How can you pass data form children to parent. Give examples
  Following are the steps to pass data from child component to parent component:

- In the parent component, create a callback function. This callback function will retrieve the data from the child component.
Pass the callback function to the child as a props from the parent component.
The child component calls the parent callback function using props and passes the data to the parent component.

5. How can you pass data form children to parent. Give examples

```js
import React from 'react';
import Child from './Child'
class App extends React.Component{
	
	state = {
		name: "",
	}

	handleCallback = (childData) =>{
		this.setState({name: childData})
	}

	render(){
		const {name} = this.state;
		return(
			<div>
				<Child parentCallback = {this.handleCallback}/>
				{name}
			</div>
		)
	}
}
export default App

import React from 'react'
class Child extends React.Component{
	
	onTrigger = (event) => {
		this.props.parentCallback(event.target.myname.value);
		event.preventDefault();
	}

	render(){
		return(
		<div>
			<form onSubmit = {this.onTrigger}>
				<input type = "text"
				name = "myname" placeholder = "Enter Name"/>
				<br></br><br></br>
				<input type = "submit" value = "Submit"/>
				<br></br><br></br>
			</form>
		</div>
		)
	}
}
export default Child
```

#### After completing this checkpoint. Schedule a call with me by using the link you will get after completing this block.