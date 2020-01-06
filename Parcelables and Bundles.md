# Parcelables and Bundles

## Sending data between activities

When sending data via an intent, you should be careful to limit the data size to a few KB. Sending too much data can cause the system to throw a `TransactionTooLargeException` exception

