# architectural tools and patterns

[MVC、MVP、MVVM，我到底该怎么选？](https://juejin.im/post/5b3a3a44f265da630e27a7e6#heading-0)

[Android 架构设计：MVC、MVP、MVVM和组件化](https://juejin.im/post/5b7c1706f265da436d7e408e)

[ViewModels and LiveData: Patterns + AntiPatterns](https://medium.com/androiddevelopers/viewmodels-and-livedata-patterns-antipatterns-21efaef74a54)

+ ViewModels  presenters
  + shouldn’t know anything about Android
  + Avoid references to Views in ViewModels
    + The recommended way to communicate between ViewModels and Views is the observer pattern, using LiveData or observables from other libraries
  + Distribute responsibilities, add a domain layer if needed
  + Expose information about the state of your data using a wrapper or another LiveData
    + [We recommend you treat your events as part of your state ？？？](https://medium.com/androiddevelopers/livedata-with-snackbar-navigation-and-other-events-the-singleliveevent-case-ac2622673150)
  + Leaking ViewModels
    + [Consuming REST API using Retrofit Library with the help of MVVM, Dagger 2, LiveData and RxJava 2 in Android](https://medium.com/@saquib3705/consuming-rest-api-using-retrofit-library-with-the-help-of-mvvm-dagger-livedata-and-rxjava2-in-67aebefe031d)
+ Activities or Fragments
  + Conditional statements, loops and general decisions should be done in ViewModels or other layers of an app, not in the Activities or Fragments
  + Views should only know how to display data and send user events to the ViewModel (or Presenter)
  + Instead of pushing data to the UI, let the UI observe changes to it
+ data repository
  + Add a data repository（ completely unaware of your presentation layer） as the single-point entry to your data