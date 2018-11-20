---?color=lavender
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

@[1,2](Import dependencies for a class)
@[4-8]
@[10-16]
@[17-25]
@[26-34]

@snap[north-east template-note text-gray]
windowSize.js
@snapend