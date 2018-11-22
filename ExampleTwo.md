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
                if (res.error === 'jwt expired') {
                    localStorage.removeItem('token');
                    this.props.dispatch({type: 'ASSIGN_USER', data: {}})
                    this.setState({
                        loading: false
                    })
                } else if (!res.error) {
                    this.setState({
                        data: res.data,
                        loading: false
                    })
                    if(res.action) {
                        this.props.dispatch({type: res.action, data: res.data});
                    }
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
@[7-12](The state is initialized with a value that determines whether or not the component is **loading** data.  The second is a spot for the actual data.)
@[14-17](Once the component is mounted it will set the state.loading to true and will fire off the fetch request to the API endpoint.)
@[18-24](For my program, if the server responds that the JWT token is expired, then I will empty my local storage.)
@[25-33](Once my data is loaded it will assign it to the state and set the loading back to being false.  If my server responds with an action key value pair, I will then send the data off to my redux store.)
@[37-40](My HoC will return the BaseComponent with the updated state.)


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