---
sidebar_position: 1
sidebar_label: Introduction
---
# Introduction To UI Components , Pages and Styling Conventions

> Components Documentation

## Conditional Rendering

[`React Docs`](https://reactjs.org/docs/conditional-rendering.html)

Example from Home.jsx

```javascript
{ user ? <WelcomeBox props={user}}/> : <Loading text=' loading Greeting'/>}
```

## Smart & Dumb Components

We Follow the Presentational and Container components principles.

### Presentational Components

Presentational components are concerned with how things look,
Presentational Components are already `Styled` or accepts a _`Style prop`_
Example `Loading Component` has default styling and accepts a _`Style prop`_ .
Presentational Components are not aware of the state of the app but can accept props that alters thier behavior
Example Presentational Component

```javascript
const component = ({styled}) => {
  const fn =  getText(text) 
  const [state , setState] = useState() //can be Statefull
  if(styled){
   setState("Presentational Component can be statefull")
  }
  return styled ? (
   <StyledDiv>{fn ?? state}<StyledDiv>
  ): <div> {fn ?? state} <div>

}
```

### Container Components

Container components are more concerned with how things work. Container components are components that specify the data a presentational component should render.

We have sorted our components accordingly
you will find all Presentational Components in the  `Components Folder` whilst Container Components are in the `Pages Folder`

### Summary
---

- Container components have to do with with how things work.

- Container Components may contain presentational components. Presentational components don’t contain container components.
- Container Components provides data and behavior to presentational components and other container components.
- Container Components are often stateful because they are mostly data sources but Presentational Component can be stateful too
