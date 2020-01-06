# Display paged lists

## Connect your UI to your view model

PagedList is content-immutable. This means that, although new content can be loaded into an instance of PagedList, the loaded items themselves cannot change once loaded. As such, if content in a PagedList updates, the PagedListAdapter object receives a completely new PagedList that contains the updated information

## Diffing using a different adapter type

If you choose not to inherit from PagedListAdapter—such as when you're using a library that provides its own adapter—you can still use the Paging Library adapter's diffing functionality by working directly with an AsyncPagedListDiffer object 

????

## Provide placeholders in your UI