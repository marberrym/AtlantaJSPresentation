# <div align="center">**React.js** - Higher Order Components
#### <div align="center">*An introduction to HoC's and smart coding.*
> **<div align="center">"Code smarter, not harder."</div>**

## <div align="center">**Who am I?**


*My name is **Matthew Marberry**.  I've spent most of my life working in the Hospitality Management industry.  I developed websites on a freelance basis using HTML/CSS and Vanilla JS for many years.  Recently I wanted to become a true developer, so I pursued further education at DigitalCrafts in Atlanta.  My coding capabilities have increased exponentially.*

<div align="center">  

### [**Portfolio**](https://www.matthew-marberry.com)

### [**Linked In**](https://www.linkedin.com/in/matthewmarberry)

</div>

## <div align="center">**What is this talk about?**

*You can view the presentation* [**here**](https://gitpitch.com/marberrym/Atlanta-Javascript-Presentation).

*This talk is going to be a brief dive into higher order components, also known as pure functions in a React.js environment.*

*A HoC is a function that takes in a component as an argument and returns a new copy of that component with additional props.*

**Benefits of using HoCs:**
* Conserve time and effort.
* Eliminate hundreds of lines of code from your application!
* Become involved in the open-source community.
* Understand some of the magic!

**What you'll get from this talk:**
* A **hopefully** better understanding of HoC's.

## <div align="center"> **The most infamous HoC**
If you're familiar with Redux and state management in a React.js environment then you already know of the most widely used HoC - the connect function.

What does connect do?

```javascript
connect({ parameters })({ component })

connect(state => ({user: state.user})(BaseComponent)
```
The connect function is one that is invoked twice, the first time it takes any parameters. In this example we use them to retrieve the user object from our Redux store.  The second time connect is invoked it takes a BaseComponent as an argument, this component will be returned with the additional prop of user. 

## <div align="center"> **Can we really make our own HoCs?**
**<div align="center">Yes, yes we can.</div>**

1. HoC Example 1: **windowSize**
<br>The need for a HoC that would wrap around a component and return that component with the **screenWidth** and **screenHeight** as props is what initially got me so interested in HoCs.  I wanted something that would allow me to change the actual content displayed on the my navBar based on size of the window.  This was an issue that couldn't be solved with css media queries - but I knew that I could develop my own HoC to suit my needs.
    
    **<div align="center">The Code:</div>**

    ```javascript
    import React, { Component } from 'react';

    export default (BaseComponent) => 
        class WindowSize extends Component {
            constructor(props) {
                super(props)
                this.state = {
                    screenWidth: window.innerWidth,
                    screenHeight: window.innerHeight
                }
            }
            
            componentDidMount() {
                window.addEventListener('resize', () => {
                    this.setState({
                        screenWidth: window.innerWidth,
                        screenHeight: window.innerHeight
                    })
                })
            }

            render() {
                return <BaseComponent 
                    {...this.state}
                    {...this.props}
                    />
            }

        }
    ```

2. HoC Example 2: **injection**
<br>This next example has allowed me to remove ***ENORMOUS*** amounts of code from my current React projects and for that I will be forever thankful.  Prior to thinking about injecting data from a ***modular*** and ***resuable*** mindset, I found myself either writing fetch requests directly inside of my classes, or making several **inject** functions to inject different data from different API endpoints.  When I was finally able to wrap my head around creating a reusable inject function, I was able to eliminate hundreds of lines of code (and we all love that right!)

    **<div align="center">The Code:</div>**

    ```javascript
    import React, { Component } from 'react';
    import url from './globalURL';

    export default (path, parameters) => (BaseComponent) => 
        class Injection extends Component {
            constructor(props) {
                super(props)
                this.state = {
                    loading: false,
                    data: {}
                }
            }

            componentDidMount() {
                this.setState({loading: true})
                fetch(url + path, parameters)
                .then(res => res.json())
                .then(res => {
                    if (res.error === 'jwt expired') {
                        localStorage.removeItem('token');
                        this.setState({
                            loading: false
                        })
                    } else if (!res.error) {
                        this.setState({
                            data: res,
                            loading: false
                        })
                        if(res.action) {
                            this.props.dispatch({type: res.action, data: res.data});
                        }
                    }
                })
            }

            render() {
                return <BaseComponent {...this.state.loading}/>
            }
        }
    ```






*You can view the presentation* [**here**](https://gitpitch.com/marberrym/Atlanta-Javascript-Presentation).

