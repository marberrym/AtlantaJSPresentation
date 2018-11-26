---?image=template/img/bg/gray.jpg&position=bottom&size=100% 15%


```js
render() {
    return props.loading ?
        <LoadingSpinner />
    :
        <GoalList {...props}/>
}

export default connect()(inject('/goal', {
    method: 'GET',
    headers: {token: localStorage.token}
})(MyGoalsSmart));
```
@[1-6](Determine whether or not to render the **LoadingSpinner** component based on if **props.loading is true.**)
@[8-11](Export our **BaseComponent** passed into our **inject HoC**)

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

@snap[west text-black span-50 recap-slide]
@ul
- Any component passed into @css[text-blue](**inject HoC**) will have have access to the specified API call.
- We can use this to load pertinent data @css[text-blue](**on any page**) after the component is mounted.
    - Username/Avatar
    - A list of goals.
    - A list of commented threads.
    - A list of friends.
- Can render a @css[text-blue](**loading component**) on the screen while the API call is being completed.
@ulend
@snapend

@snap[east]
<iframe src="https://giphy.com/embed/3ohzdIuqJoo8QdKlnW" width="480" height="222" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/reactionseditor-yes-awesome-3ohzdIuqJoo8QdKlnW"></a></p>
@snapend