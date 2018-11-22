---?image=template/img/bg/gray.jpg&position=bottom&size=100% 15%
@title[HoC Example 1]

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

@[1](Import dependencies for creating a React class)
@[3-6](Here we are exporting a function that will take in one argument: **BaseComponent**, then this function creates a class wrapped around our **BaseComponent** called **WindowSize**)
@[7-9](The **WindowSize** class will be initialized with a state that uses the initial values for the inner width and height of the window.)
@[13-20](After the component is mounted it adds an event listener on the window.  Every time it is resized it will update the values in the state of **WindowSize**)
@[22-28](Our wrapper class will then return the **BaseComponent** with the state of **WindowSize** and any props it may have)

@snap[south text-white span-100 footer]
@fa[fab fa-github-square margin-sides]
@size[.4em](marberrym)
@fa[fab fa-linkedin margin-sides]
@size[.4em](Matthew Marberry)
@fa[envelope-o margin-sides]
@size[.4em](marberrym@gmail.com)
@fa[globe margin-sides]
@size[.4em](matthew-marberry.com)
@snapend

@snap[north-east template-note text-gray]
windowSize.js
@snapend