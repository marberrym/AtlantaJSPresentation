---?color=lavender
@title[HoC Example 1]

```javascript
//Importing neccessary dependencies from React Library
import React, { Component } from 'react';

//Creating a HoC that takes in a Component as an arguement
export default (BaseComponent) => 
    class WindowSize extends Component {
        constructor(props) {
            super(props)

            //Initiates the state's screenWidth and screenHeight as the initial innerWidth and innerHeight of the window
            this.state = {
                screenWidth: window.innerWidth,
                screenHeight: window.innerHeight
            }
        }
        
        //Adds an event listener on the Window - when it is resized it will reassign the screenWidth and screenHeight in state
        componentDidMount() {
            window.addEventListener('resize', () => {
                this.setState({
                    screenWidth: window.innerWidth,
                    screenHeight: window.innerHeight
                })
            })
        }

        //This will return the BaseComponent with additional states and props.
        render() {
            return <BaseComponent 
                {...this.state}
                {...this.props}
                />
        }
    }
```

@[1,2]
@[4-8]
@[10-16]
@[17-25]
@[26-34]

@snap[north-east template-note text-gray]
windowSize.js
@snapend