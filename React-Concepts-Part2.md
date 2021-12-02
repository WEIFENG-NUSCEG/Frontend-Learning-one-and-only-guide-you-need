# React Concepts Part.2 - The one and only guide you need


_"I'm just summarizing my React learning routine here and this is the second part,your follow will be my motivation to update. Hope it will help you to improve your understanding towards React as well. Noted that the React version discussed here starts from 16.8 onwards. Concept such as HOC and class components are not included. (updates regularly)"_ </br>
</br>
</br>
</br>
## Table Of Contents 
[1. What are the Lifecycle of Components?](#c1)</br>
[2. React Hooks in Function components](#c2)</br>

- [2.1 The differences between Function components and Class components](#c21)

- [2.2.Why are we using array instead of object in `useState()`](#c22)

- [2.3 What problems have been solved by Hooks](#c23)

- [2.4 Rule of Hooks](#c24)

- [2.5 Difference between useEffect and useLayoutEffect](#c25)

- [2.6 Relationship between life cycle and hooks](#c26)</br>

[3. Difference between React.map and JS.map](#c3)</br>
[4. Why are we using JSX](#c4)</br>
[5. Communication between Components](#c5)</br>
[6. React Routers (In progress)](#c6)</br>

- [6.1 Client router concept](#c61)

- [6.2 Switch between different routes](#c62)

- [6.3 Redirection in React Router](#c63)

- [6.4 Redirection in React Router](#c64)</br>

[7. Redux (Coming soon)](#c7)
</br>
</br>
</br>
## Other Contents
[React Concepts Part.1 - The one and only guide you need](https://dev.to/weifengnusceg/my-frontend-developer-learning-route-react-in-progress-10ki)
[HTML - The one and only guide you need (in progress)](https://dev.to/weifengnusceg/my-frontend-developer-learning-route-html-3mga)
[](url) </br>
</br>
</br>
</br>

### 1. What are the Lifecycle of Components? <a name="c1"></a>

> Each component in React has a lifecycle which you can monitor and manipulate during its three main phases.
> The three phases are: Mounting, Updating, and Unmounting.

  1. Mounting means putting elements into the DOM.

  2. The next phase in the lifecycle is when a component is updated. A component is updated whenever there is a change in the component's state or props.

  3. The next phase in the lifecycle is when a component is removed from the DOM, or unmounting as React likes to call it.

![React Life Cycle](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/k4dhywfr73ze9fi3dft8.png)

### 2. React Hooks in Function components <a name="c2"></a>

**2.1 The differences between Function components and Class components** <a name="c21"></a>

(Before hooks was introduced)
- Inital Class components need to extends from `React.Component`, function components do not need to do so </br>
</br>
- Class components can access life cycle methods, but function components cannot. </br>
</br>
- Class components can access the this in the instantiated object. </br>
</br> 
- Function components can't define and manage the state

The key concept of designing React component is to treat it as function, a function that inputs data and outputs UI. It convert our declarative code into imperative DOM. Data and renders should be bind together. Function Component has achieved this in version 16.8 with the help of Hooks.

**2.2 Why are we using array instead of object in `useState()`** <a name="c22"></a>

- By using array destructuring, we can give any name to the variables in the array.

- If we are using object destructuring, we have to use the identical name to the retrieved object's property name.

**2.3 What problems have been solved by Hooks** <a name="c23"></a>

The use of hooks reduces the number of concepts needed in the development of React applications, hooks offer us homogeneity in the ecosystem. And React lifecycle has been greatly simplified.

Hook extracts state logic from components so that these logics can be tested and reused separately. Hook allows us to reuse state logic without modifying the component structure. This makes it easier to share Hooks between components or within the community.

**2.4 Rule of Hooks** <a name="c24"></a>

- Only Call Hooks at the Top Level, Do not call Hooks in loops, conditions, or nested functions

- Only Call Hooks from React Functions, Do not Call Hook in Javascript's functional component.

**2.5 Difference between useEffect and useLayoutEffect** <a name="c25"></a>

- `useEffect` will be called asynchronously during rendering that runs after react has rendered all the components to
ensures that effect callback does not block browser painting. It change the DOM after rendering which results to screen to blinking.

- useLayoutEffect runs synchronously immediately after React has performed all DOM mutations and then proceed to rendering, hence avoid using it with heavy calculation callbacks which may block the UI display. It can be useful if you need to make DOM measurements such as the scroll position or DOM mutations.


**2.6 Relationship between life cycle and hooks** <a name="c26"></a>

| Class Components| Hooks |
| --------- |:---------:|
| `getDerivedStateFromProps` | `useState`'s update function | 
| `shouldComponentUpdate` | `useMemo` | 
| `componentDidMount` | `useEffect` with empty dependency | 
| `componentDidUpdate` | `useEffect` | 
| `componentWillUnmount` | `useEffect`'s return function |


### 3. Difference between React.map and JS.map <a name="c3"></a>

The map method in Javascript will not process the null and undefined values. However React.child.mao will handle them in some situation.

### 4. Why are we using JSX <a name="c4"></a>

```
return React.createElement(
        'div',
        null, 
        `Hello ${this.props.toWhat}`
      );
```

JSX is a syntax extension of JavaScript for `React.createElement()` method. Using XML will have a better readability.

### 5. Communication between Components <a name="c5"></a>

1. From parent to child components: Use props to pass data.

2. From child to parent components: Use props to pass the callback function and let the child component to call the function.

3. Use context or Redux to handle global states cross levels.

4. Use Event subscriber model: Listener subscribe to the events from publisher and respond accordingly.


### 6. React routers (In progress...)<a name="c6"></a>

**6.1 Client router concept** <a name="c61"></a>

- Hash-based routing: Listening to `hashChange` event. We can directly change hash by assign variable to location.hash

- Based on HTML5 history lib: We can change URL by `history.pushState`. 


**6.2 Switch between different routes** <a name="c62"></a>

- Use the `<Route>` Component

- Use `<Switch>` with `<Route>`

- Use `<Link>`、 `<NavLink>`、`<Redirect>` components


**6.3 Redirection in React Router** <a name="c63"></a>

- Use `<Redirect>` component

**6.4 Redirection in React Router** <a name="c63"></a>
