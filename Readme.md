# How to hook ReactJs to your existing AngularJS 1.X app

This repository shows how you can use ReactJs in your existing AngularJS 1.X app.

----------

Preface
ReactJs and Angular 2.0 are really trending now in the UI world. But what about apps which where created by Angular 1.x. Is there any way to hook react or Angular 2.0 into an existing Angular 1.x app?

There are so many apps which are developed with Angular 1.x.

And teams would be struck with so many questions like:
So what do we do with future developments, do we still continue using Angular 1.x or do we slowly start migrating to a newer framework?
What if that framework gets obsolete tomorrow and we have to migrate again to a newer one?
Or is it really feasible to redo the entire app with newer framework?
Is there a way I can keep my current AngularJs 1.x stack and slowly add the future releases of my app using newer libraries/frameworks?
How do I pass data between AngularJs and the new library that I use?
I will show you how to hook ReactJs to your AngularJS 1.X app in this article.
ReactJS is only a library which is used for the View part of MVC or MVV or whatever and this got me thinking why don’t I try hooking ReactJs into an AngularJs 1.x app?

This article here just covers on how to hook ReactJS into an existing AngularJs 1.x app to handle only the view and at this point I haven’t considered adding Redux.

A basic To-Do app created in Angular 1.x and hooking React into it.

This app will give you an idea on how you can pass values from your Angular app to React and also the other way around from React to Angular
What does this app do?
This app creates a basic TO-DO using AngularJs 1.x.
It passes any existing TO-DO from Angular to React on rendering of the page.(Passing data from AngularJs to React)
Any new item added from Angular TO- DO gets added into React TO-DO. (Passing data from AngularJs to React).
Clicking on an item in React TO-DO will mark the item as complete/incomplete in AngularJS (Passing data from React to AngularJs) and since the scope variable changes at Angular, the prop is React gets updated and therefore the item is marked complete in React To-do as well (Passing data from AngularJs to React)

Install the dependencies and devDependencies by issuing yarn install or npm install

Running the example
Just issue the below command and you are good to go 😉

yarn start or npm start

Understanding how values are passed between Angular and React
How it is done?
Angular puts JS into HTML while React puts HTML into JS. How do I marry these two? 😕

This is where you use a custom directive in Angular and bootstrap your React code inside that. This way you isolate the React code(view) from the rest.

This is great! I have bootstrapped React now and I have it in isolation, but then how do I share values between them? The subsequent sections will show you on how to pass values between them.
AngularJs to React
In the earlier section I had mentioned there are three scenarios where Angular passes values to React. Let us try to understand each of these scenario so that you get a better understanding.

During initial load of the page.
---------------------------------
In the custom directive ./src/angular/reactDirective.js we pass the todo list as an isolated scope as shown below:

scope: {
        todos: '=',
        markComplete:'&'
      }
And this todos is passed as props when we bootstrap the react app as shown below:

scope.$watch('todos', function(newValue, oldValue) {
                if (angular.isDefined(newValue)) {
                 ReactDOM.render(
                    <Layout todos={newValue} newItem={scope.newItem} markComplete={scope.markComplete}/>
                    , reactapp);
                 console.log(scope.newItem)
                }
            }, true);
We bootstrap the react app inside a scope.$watch so that each time the value of scope.todos changes, it is caught in the directive and renders our react app.

Therefore even when you add a new item in Angular To-do, since the scope.todos changes, you can see React To-do gets the new value. You can see the next section for more on this.

When a new item is added in Angular To-do
----------------------------------------------
As mentioned in the previous section, when scope.todos changes, the react component re-renders.

Probably you might be wondering here,

Do we bootstrap each time the value of todos changes?
And will all the component lifecycle get triggered from scratch in the react app?
Well it doesn’t. Bootstrap happens only on the first instance, and thereafter when ever ReactDOM.render runs, it only renders what is necessary and it will not mount everything from scratch again.

When we mark an item complete in React To-do.
------------------------------------------------
This is covered in detail in the section — React to AngularJS.

Summarizing on AngularJs to React data transfer
-------------------------------------------------
Passing values from Angular to React was pretty simple. All you had to do was:-

Create a custom directive to wrap your React app.
Pass the data from parent to the custom directive via isolated scope.
Catch the updated values in link() using scope.$watch().
Pass the values as props to the react app.

To prove this here is a screenshot with componentWillMount lifecycle hook added in with a simple console logging.

React to AngularJs
--------------------

The scenario where we pass value from React to Angular in this example is when we mark an item as complete or incomplete in the React to-do and the same should be reflected in the Angular to-do.
This is a bit tricky compared to passing from AngularJs to React.

props are read-only so you can’t directly modify them. So any change that our React app should do should come from it’s props.

This helps in keeping the data flow unidirectional in React.
To overcome this and pass the value to the Angular To-do,

We also pass a function as an isolated scope to the custom directive.
This function will be send as a prop to the react app.
When we click on any of the item in the React to-do, the prop function fires, and since this is nothing but the function from isolated scope in Angular custom directive, this function is fired. (Passing functions between Angular and React using props).
But the function in custom directive in turn fires the function in the parent because we pass the function as isolated scope. (Passing functions between directive using isolate scope)
And finally once the function in the parent Angular controller runs and updates the scope.todos, the update value is passed back as prop to the React app.
So in our case:-

Conclusion
Go ahead and give it a try!! 😀

AngularJs 1.x is still in the game and is still very popular. Last when I worked on Angular I used Angular 1.5.x and when I was creating this example I noticed that Angular 1.6.x is out, and that is what I have used here.

It’s good to see that Angular 1.x is still being updated actively even after Angular 2.0 is out.

But if you feel you have a very heavy view layer which Angular 1.x makes slow, give React a try. React is just a view library and it is so easy to plug it into any other framework as you saw above.

Until my next article…..
