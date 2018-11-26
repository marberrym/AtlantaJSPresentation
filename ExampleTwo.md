---?image=template/img/bg/gray.jpg&position=bottom&size=100% 15%
@title[HoC Example 2]

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
                if (!res.error) {
                    this.setState({
                        data: res.data,
                        loading: false
                    })
                    if(res.action) {
                        this.props.dispatch({type: res.action, data: res.data});
                    }
                } else {
                    this.setState({
                        loading: false
                    })
                }
            })
        }

        render() {
            return <BaseComponent {...this.state}/>
        }
    }
```

@[1,2](Imports necessary dependencies)
@[4-7](This HoC is a function that gets invoked **"twice"** similar to the redux connect function.  The first invocation requires two arguments, the first is the **API endpoint** and the second is the **request parameters**.  The second invocation requires one argument, **the BaseComponent**.)
@[7-12](The state is initialized with a value that determines whether or not the component is **loading** data.  The second is a spot for the **response data.**)
@[14-18](Once the component is **mounted** it will set the **state.loading** to **TRUE** and will fire the request to the **API endpoint.**)
@[19-23](Once the response is received it will assign the **response data** to state and return **state.loading** to a value of **FALSE.**)
@[24-26](If using **Redux** for **state management** then the server will respond with a **res.action** value which will be used to **dispatch** to the **Redux store.**)
@[27-31](If there is an **error** returned by the request, then **state.loading** will be returned to a value of **FALSE.**)
@[35-38](This HoC will return the **BaseComponent** with the **updated state.**)


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
injection.js
@snapend