---?image=template/img/bg/gray.jpg&position=bottom&size=100% 15%
```js
import React from 'react';
import { Link } from 'react-router-dom';
import './navBar.css';
import { connect } from 'react-redux';
import windowSize from '../windowSize';
import BurgerNav from './BurgerNav';

let NavBar = (props) =>
    <div className="navbar">
        <div className="navLinkGroup">
            <Link to="/"><img className="navBarLogo" 
            src='http://localhost:3000/images/dgdg.png' 
            alt="DGDG Logo"/></Link>
            <Link to="/" className="navLink">Home</Link>
            
            <Link to="/about" className="navLink">About DGDG</Link>
        </div>
        {localStorage.token ?
            props.screenWidth > 600 ?
                <div className="navLinkGroup">
                    <div className="avatarBox">
                        <Link to='/goals'><img className="navBarLogo navBarAvatar" 
                        src={`/uploads/avatars/${props.user.avatar}`}
                        alt="avatar"/></Link>
                    </div>
                    <Link to="/goals" className="navLink">My Goals</Link>
                    <div className="navLink" onClick={event => {
                        window.localStorage.clear()
                        props.dispatch({
                            type: "ASSIGN_USER", 
                            data: {}
                        })
                    }}>Log Out</div>
                </div>
            :
                <BurgerNav avatar={props.user.avatar} 
                dispatch={props.dispatch}/>
        :
            <div className="navLinkGroup">
                <Link to="/signup" className="navLink">Sign Up</Link>
                <Link to="/login" className="navLink">Log In</Link>
            </div>
        }
    </div>

let NavBarSmart = connect(state => ({
    user: state.user
    }))(windowSize(NavBar))
export default NavBarSmart;
```

@[1-6](**Import necessary dependencies**)
@[8-19](**Creates NavBar component**)
@[18,19](**Checks for user web token and checks the screenWidth which is passed down by out windowSize HoC**)
@[35-37](**If our screenWidth<600 the BurgerNav component will be rendered**)
@[46-49](**Passes our NavBar compenent into the windowSize HoC, then connects the resulting component to our redux store**)

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
NavBar.js
@snapend

---?image=template/img/bg/gray.jpg&position=bottom&size=100% 15%

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

@css[headline text-blue](Reusability)

@snap[north text-black]
@ul
- @size[.5em](Any component passed into @css[text-blue](**windowSize()**) will have the window dimensions passed down as props.)
- @size[.5em](We can use this to change @css[text-blue](**which components**) will be rendered on the screen based on the window dimensions.)
- @size[.5em](Can be used to @css[text-blue](**proritize the importance**) of space and UI on mobile vs. computer.)
@ulend
@snapend

