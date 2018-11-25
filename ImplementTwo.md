---?image=template/img/bg/gray.jpg&position=bottom&size=100% 15%
```js
export default connect()(inject('/goal', {
    method: 'GET',
    headers: {token: localStorage.token}
})(MyGoalsSmart));
```

@[1-4](**Export my higher order component**)


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
MyGoals.js
@snapend