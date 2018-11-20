---?image=template/img/bg/gray.jpg&position=bottom&size=100% 15%
@title[HoC Example 2]

```javascript
//Import Dependencies
import React, { Component } from 'react';
import url from './globalURL';

//Takes in two sets of arguments invoked seperately
//First is the API endpoint, then the request parameters
//Creates wrapper class Injection with props and state
export default (path, parameters) => (BaseComponent) => 
    class Injection extends Component {
        constructor(props) {
            super(props)
            this.state = {
                loading: false,
                data: {}
            }
        }

        //Fires the fetch request once the component mounts
        componentDidMount() {
            //Loading is equal to true
            this.setState({loading: true})
            //Fetches from the endpoint
            fetch(url + path, parameters)
            .then(res => res.json())
            .then(res => {
                //Accounts for expired token
                if (res.error === 'jwt expired') {
                    localStorage.removeItem('token');
                    this.props.dispatch({type: 'ASSIGN_USER', data: {}})
                    this.setState({
                        loading: false
                    })
                //Sets data in the state
                } else if (!res.error) {
                    this.setState({
                        data: res.data,
                        loading: false
                    })
                    //Dispatches to redux store
                    if(res.action) {
                        this.props.dispatch({type: res.action, data: res.data});
                    }
                }
            })
        }
        //Returns BaseComponent
        render() {
            return <BaseComponent {...this.state.loading}/>
        }
    }
```

@[1-3]
@[5-16]
@[18-25]
@[26-32]
@[33-45]
@[46-50]

@snap[south text-white span-100]
@fa[fab fa-github-square]
@size[.4em](marberrym)
@fa[fab fa-linkedin]
@size[.4em](Matthew Marberry)
@snapend

@snap[north-east template-note text-gray]
injection.js
@snapend