# React Concepts Part.1 - The one and only guide you need


_"I'm just summarizing my React learning routine here, your follow will be my motivation to update. Hope it will help you to improve your understanding towards React as well. Noted that the React version discussed here starts from 16.8 onwards. Concept such as HOC and class components are not included. (updates regularly)"_ </br>
</br>
</br>
</br>
## Table Of Contents 
[1. Why do we choose to use React?](#c1)</br>
[2. React Synthetic Events](#c2)</br>
[3. Why should we use hooks in React?](#c3)</br>
[4.How do we understand React-Fiber and what problems has it solved?](#c4)</br>
[5. What's the difference between Component and Element](#c5)</br>
[6.When will component rerender in react?](#c6)</br>
[7. What will happen during re-rendering](#c7)</br>
- [7.1 What is React key?](#c71)</br>

[8. Stateless Component](#c8)</br>
[9. How to get the DOM element in React 16.8?](#c9) </br>
[10. React Portals](#c10) </br>
[11. How to avoid unnecessary re-renders in React 16.8?](#c11) </br>
[12. The mechanism behind React context](#c12) </br>
[13. Uncontrolled Components](#c13) </br>
</br>
</br>
</br>


### 1. Why do we choose to use React? <a name="c1"></a>

**- It allows server-side rendering.**

Server-side rendering (SSR) is an application’s ability to convert HTML files on the server into a fully rendered HTML page for the client.

  **Pros**

  1. A server-side rendered application enables pages to load faster, improving the user experience.

  2. Search engines can easily index and crawl content because the content can be rendered before the page is loaded, which is ideal for SEO

  3. Rendering server-side helps efficiently load webpages for users with slow internet connection or outdated devices.

  **Cons**

  1. Rendering static HTML from server-side is efficient, but for complex applications with frequent server requests and full page reloads can increase load times due to the bottleneck of the server performance. It can be very costly and pressuring the server.

  2. Server-side rendering may not be compatible with third-party JavaScript code

**- It uses the virtual DOM instead of the real DOM.**

React use _batch update mechanism_ to update the real DOM. Hence, leading to increased performance. This means that updates to the real DOM are sent in batches, instead of sending updates for every single change in state as Frequent DOM manipulations are expensive and performance heavy.

React virtual DOM is updated with the state changes. The previous and current version of virtual DOM is compared through an efficient diff algorithm. 

**- It follows uni-directional data flow or data binding.**

Uni-directional data flow gives you the control over how data flows throughout your app. The data flows in a single direction from parent to child making it much more predictablef for tracing and debugging

**- It is component based and extensive.**

Component based provides React with better code maintenance and growth as each component in React has their own internal logic, which is easy to manipulate.


## **2. React Synthetic Events** <a name="c2"></a> 

> Your event handlers will be passed instances of SyntheticEvent, a cross-browser wrapper around the browser’s native event.

Synthetic events are delegated to document instead of the real DOM node. Therefore native events are triggered first and the events bubble up to doucment, after which the synthetic events are triggerd.

  1. It provides better cross-browser compatibility as it provides a uniform api and consistent behavior on top level.

  2. It provides better performance as for the native broswer events, the browser will create a new event object for the listener and bind it to the node. If we have multiple listener, multiple objects will be created and require a lot of resources from the memory. 

  However, the synthetic events objects are pooled and managed together. SyntheticEvent object will be reused and all properties will be nullified after the event handler has been called. 

To stop the native broswer event from bubbling, we should use event.preventDefault()


## **3. Why should we use hooks in React?** <a name="c3"></a> 

  1. Hooks are easier to work with and to test.


  2. Code looks cleaner, easier to read. 


## **4.How do we understand React-Fiber and what problems has it solved?** <a name="c4"></a>

In previous React Engines' rendering process (V15), it will recursively compare the virtual DOM's change and update to the real DOM in one shot. This process wouldn't stop in any case. The events triggered by users such as inputting text will not be respond as browser's resources are occupied which cause lagging and drop in frame.

To improve this, Fiber now allows React to pause, resume, and restart the work on a component. It has a priority-based update system which allows the React to fine tune the renderer process.

However fiber is not equal to thread. It represents a mechanism to give up the execution rights of the CPU so that the CPU can perform other operations during this time. The rendering process can be interrupted and control can be returned to the browser, giving way to high-priority tasks such as user triggered events, and rendering can be resumed when the browser is idle.


## **5. What's the difference between Component and Element** <a name="c5"></a>

  1. Element: An element is a plain object describing a component instance or DOM node and its desired properties. It is a way to tell React what you want to see on the screen. They are not the actual instances. 

  2. Component: Component encapsulate element trees, but generally it can be deemed as a function which takes props as arguments and return a Element tree.

(Never create a instance, React will help us do it)


## **6.When will component rerender in react?** <a name="c6"></a>

React components re-render whenever there is a change in their state or props. 

A simple update of the state (e.g using `setState()`), causes the component and all its child components to be re-rendered automatically.


## **7. What will happen during re-rendering** <a name="c7"></a>

- Recursively Compare the previous VDOM with the current VDOM by DIFF algorithm. (using DFS to traverse every node, put the difference in an object if there is any.)

React's basic concept for processing renders is to re-render the entire application whenever there is a change. It is not saying that Virtual DOM is faster than direct manipulation of the DOM

No matter how the data changes, it will try to update the DOM with the least cost. When the DOM tree is huge, traversing the previous and current trees is still quite expensive, especially when it is just a small modification at the top level by `setState()` leads to traversing the entire tree by default. (We can improve this by using memo hooks)

**7.1 What is React key?** <a name="c71"></a>

Keys are identifiers used by React to track which elements in the list have been modified, added, or removed. During the development process, we need to ensure that the key of an element is unique among its sibling elements.

In the React Diff algorithm, React will use the Key value of the element to determine whether the element is newly created or moved, thereby reducing unnecessary element re-rendering

- key must be unique to each element in the array

- do not use the index

- do not use an unstable key such as random number



## **8. Stateless Component** <a name="c8"></a>

A stateless component has no state (:)), it means that you can’t reach `this.state` inside it. It also has no lifecycle so you shouldn't use those methods and hooks.


## **9. How to get the DOM element in React 16.8?** <a name="c9"></a> 

`const refContainer = useRef(initialValue);`

> `useRef` returns a mutable ref object whose .current property is initialized to the passed argument (initialValue). The returned object will persist for the full lifetime of the component.

```
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    // `current` points to the mounted text input element
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

We can't visit the refs during render phase as the DOM has not been stablished.

![React Life Cycle](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/81seqdla55r4bsrnhoip.png)

## **10. React Portals** <a name="c10"></a>
 

> Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.

`ReactDOM.createPortal(child, container)`

Elements need to be insert into a different location in the DOM. A typical use case for portals is when a parent component has an overflow: hidden or z-index style, but you need the child to visually “break out” of its container. For example, dialogs, hovercards, and tooltips.

An event fired from inside a portal will propagate to ancestors in the containing React tree, even if those elements are not ancestors in the DOM tree. 


## **11. How to avoid unnecessary re-renders in React 16.8 ?** <a name="c11"></a>

React.memo is a new API comes from React 16.6. It is used to cache component rendering and avoid unnecessary updates. It is a high-level component that's very similar to PureComponent. The difference is that React.memo can only be used for functional components.


## **12. The mechanism behind React context** <a name="c12"></a>

We can use the Javascript clousure as an analogy, the Context object provided by the React component is actually like a clousure provided to child components to access. The properties of the Context object can be regarded as active objects in the scope. 

Since the Context of a component is composed of all the components on the parent node chain through `getChildContext（）`, the Context object returned by the component can access the Context properties from all its parent component.


## **13. Uncontrolled Components** <a name="c13"></a>

> In most cases, we recommend using controlled components to implement forms. In a controlled component, form data is handled by a React component. The alternative is uncontrolled components, where form data is handled by the DOM itself.

> Since an uncontrolled component keeps the source of truth in the DOM, it is sometimes easier to integrate React and non-React code when using uncontrolled components. It can also be slightly less code if you want to be quick and dirty. Otherwise, you should usually use controlled components.






 
