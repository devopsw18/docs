---
sidebar_position: 0
sidebar_label: Container
---
# Container

# Using the container component to write conposable and responsive styling

The container component main responsibility is to wrap our pages and other component for easy manipulation.
be it styling or handling user interactions.
In our case it is mainly used for styling so how do we use it and what does it solve?
The container component accepts two props `customStyles` & `children`.
The  `children` are its children in the react dom. we do not need to explicitly express them react takes care of this for us 
so when we write code like this

```javascript
const PageToCompose = () => {
  return (
    <Container>
    <PageContent/>
    </Container>
  )
}
```

PageContent is passed to our container as a child property and in our case it also conforms to our containers  default styling which is

```css
.container {
  display : flex;
  flex-direction : column;
  align-items : center;
  width : 100%
}

```

This centers our `PageContent`.

The power of this architecture for Styling is the `customStyles` here we can customize our container as we see fit. and this only affect that instace of the container, so we can use the container in different places.

Each instace of our component can now be receive custom styling fot its specific use case and we could take it a sted further and make this a Higher order component but that is beyond this scope of this.
For example on a HOC take a look at `Protected Routes`

## So how does this make our App more responsive?

Before we can understand this we need to first understand css specifically flexbox
flexbox on its own is very powerful tool with flexbox you can create simple yet responsive design in a matter of minutes.
Our container components should be taking advantage of this. combined with a hook like useMediaQuerry we can style our components and create beutiful responsive application with minimal effort.
This means we dont have to write media querries on a component or page level but on the container level taking advantage of our components interoperability.

```javascript
const OnMobile = () =>{ 
    const mobile = useMediaQuery('(max-width: 920px)');
    
    const mobileStyle = { width: 10px}
    const destopStyle = { width: 100px}
    return ( 
      <Container customStyle={mobile? mobileStle : destopStyle}>
      <CoolComponent>
      </Container>
    )
}
```

CoolComponent should now adhere to it parent and contained in our container, This approach is ofcourse applicable on any level we see fit.

```javascript
const CoolComponent = () =>{ 
    const mobile = useMediaQuery('(max-width: 920px)');
    
    const mobileStyle = { width: "blue"}
    const destopStyle = { color: "red"}
    return ( 
      <h1> Hello </h1>
      <p style={mobile? mobileStyle : destopStyle}>{mobile ? "Nice Phone" : "Cool Computer }</p>
    )
}

```

But since we have consistent design across devices this is not required nor needed.

## Why?

- We avoid magic. By magic i mean not being able to explain why things are happeing in our app. We had this issue in the old code base when there were lots of mediaqueries everywhere for everything this is not necessary with this approach we can achieve very concise, responsive and consistent behavior.

- Our components become composable and makes it easier to do more advance operations with ease where and if needed.

- We style the components as they need to be not as they want to be. We design mobile first and that design should be as is we should not alter that to accomadate any other screen size our design on the mobile should be impecable then we can scale accordingly.

- A approachable pattern that brings clarity and relatively easy to build and build upon.

- We build the mobile first then adapt. you dont have to think about desktop when writing your components. use flexbox and make sure the are  composable. example `<DateComponent/>` should look and act the same if i put on `Patient Profile` or  `Book Consultation`. it should not matter where your component is rendered they should always look the same way.
- Promotes good health

For more information i will recommend to look att mui and other design systems examples of useMediaQuerry or give it a try now with this [Npm package](https://www.npmjs.com/package/react-responsive)
