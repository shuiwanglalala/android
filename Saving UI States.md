# Saving UI States

## Options for preserving UI state



[ViewModels: Persistence, onSaveInstanceState(), Restoring UI State and Loaders](https://medium.com/androiddevelopers/viewmodels-persistence-onsaveinstancestate-restoring-ui-state-and-loaders-fc7cc4a6c090)

- Do ViewModels persist my data?
  - ViewModels hold transient data used in the UI but they don’t persist data
- Are ViewModels a replacement for onSaveInstanceState?
  - onSaveInstanceState()
    - retain a small amount of UI related data in two situations
      - The app’s process is stopped when it’s in the background due to memory constraints
      - Configuration changes
    - onSaveInstanceState() is called in situations in which the activity is stopped, but not finished, by the system. It is not called when the user explicitly closes the activity or in other cases when finish() is called
  - Fragment.setRetainInstance(true)
    - The usefulness of creating a retained fragment is that it’s meant to retain large sets of data such as images or to retain complex objects like network connections
  - ViewModel
    - ViewModels only survive configuration change-related destruction; they do not survive the process being stopped. This makes ViewModels a replacement for using a fragment with setRetainInstance(true) (in fact ViewModels use a fragment with setRetainInstance set to true behind the scenes)
- How do I use ViewModels to save and restore UI state efficiently
  - ?????