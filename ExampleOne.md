---?image=template/img/bg/gray.jpg&position=bottom&size=100% 15%
@title[HoC Example 1]

```javascript
//Import Dependencies
import React, { Component } from 'react';

//Takes in Component as Arguement
export default (BaseComponent) => 
    class WindowSize extends Component {
        constructor(props) {
            super(props)

            //Innitiates State
            this.state = {
                screenWidth: window.innerWidth,
                screenHeight: window.innerHeight
            }
        }
        
        //Changes State on Resize
        componentDidMount() {
            window.addEventListener('resize', () => {
                this.setState({
                    screenWidth: window.innerWidth,
                    screenHeight: window.innerHeight
                })
            })
        }

        //Returns Base Component
        render() {
            return <BaseComponent 
                {...this.state}
                {...this.props}
                />
        }
    }
```

@[1,2](Import dependencies for creating a React class)
@[4-8](Here we are exporting a function that will take in one argument: **BaseComponent**, then this function creates a class wrapped around our **BaseComponent** called **WindowSize**)
@[10-16](The **WindowSize** class will be initialized with a state that uses the initial values for the inner width and height of the window.)
@[17-25](After the component is mounted it adds an event listener on the window.  Every time it is resized it will update the values in the state of **WindowSize**)
@[26-34](Our wrapper class will then return the **BaseComponent** with the state of **WindowSize** and any props it may have)

@snap[south text-white span-100 footer]
@fa[fab fa-github-square]
@size[.4em](marberrym)
@fa[fab fa-linkedin]
@size[.4em](Matthew Marberry)
<img src="/template/img/MMLogoColored.png" class="logo">
@size[.4em](matthew-marberry.com)
@snapend

@snap[north-east template-note text-gray]
windowSize.js
@snapend