# Defining your Work Requests

## Work constraints

When multiple constraints are specified, your task will run only when all the constraints are met

In the event that a constraint fails while your task is running, WorkManager will stop your worker. The task will then be retried when the constraint(s) are met

## Initial Delays

The exact time that the worker is going to be executed also depends on the constraints that are used in your WorkRequest and on system optimizations. WorkManager is designed to give the best possible behavior under these restrictions

## Defining input/output for your task

Data objects are intended to be small and values can be Strings, primitive types, or their array variants. If you need to pass more data in and out of your Worker, you should put your data elsewhere, such as a Room database. There is a maximum size limit of 10KB for Data objects