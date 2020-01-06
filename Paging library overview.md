# Paging library overview

## Library architecture

### PagedList

The Paging Library's key component is the PagedList class, which loads chunks of your app's data, or pages. As more data is needed, it's paged into the existing PagedList object. If any loaded data changes, a new instance of PagedList is emitted to the observable data holder from a LiveData or RxJava2-based object



