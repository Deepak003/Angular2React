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

