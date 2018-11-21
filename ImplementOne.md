---?image=template/img/bg/gray.jpg&position=bottom&size=100% 15%
```javascript
//Import Dependencies
import React from 'react';
import { Link } from 'react-router-dom';
import './navBar.css';
import { connect } from 'react-redux';
import windowSize from '../windowSize';
import BurgerNav from './BurgerNav';

//Create Function
let NavBar = (props) =>
    <div className="navbar">
        <div className="navLinkGroup">
            <Link to="/"><img className="navBarLogo" src='http://localhost:3000/images/dgdg.png' alt="DGDG Logo"/></Link>
            <Link to="/" className="navLink">Home</Link>
            
            <Link to="/about" className="navLink">About DGDG</Link>
        </div>
        {
        //Checks for token then checks the screenWidth
        localStorage.token ?
            props.screenWidth > 600 ?
                <div className="navLinkGroup">
                    <div className="avatarBox">
                        <Link to='/goals'><img className="navBarLogo navBarAvatar" src={`/uploads/avatars/${props.user.avatar}`} alt="avatar"/></Link>
                    </div>
                    <Link to="/goals" className="navLink">My Goals</Link>
                    <div className="navLink" onClick={event => {
                        window.localStorage.clear()
                        props.dispatch({type: "ASSIGN_USER", data: {}})
                    }}>Log Out</div>
                </div>
            :
                //If screenWidth < 600 render BurgerNav
                <BurgerNav avatar={props.user.avatar} dispatch={props.dispatch}/>
        :
            <div className="navLinkGroup">
                <Link to="/signup" className="navLink">Sign Up</Link>
                <Link to="/login" className="navLink">Log In</Link>
            </div>
        }
    </div>
       
//Connect windowSize(NavBar) to redux
let NavBarSmart = connect(state => ({user: state.user}))(windowSize(NavBar))
export default NavBarSmart;
```

@[1-7]
@[9-18]
@[19-32]
@[32-41]
@[43-45]

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