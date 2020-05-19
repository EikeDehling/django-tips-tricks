# Transactions and Locking

With Django being a web framework, there is often multiple users, their actions can potentially interact and/or conflict.

To keep data consistent and avoid undesirable bugs, we can use transactions and lock the objects we're working on.  Locking means other users can't access or change the locked object, so they can't conflict.

## Transaction middleware

To ensure we always have a transaction, we enable the transaction processing in the django settings:

```
DATABASES = [
    'default': {
        ...
        ATOMIC_REQUESTS': True
    }
]
```

## Locking helper

To lock database objects when we're about to change them, we can use this helper function:

```
def get_object_for_update_or_404(ModelClass, pk):
    try:
        return ModelClass.objects.select_for_update().get(pk=pk)
    except ModelClass.DoesNotExist:
        raise Http404('No %s matches the given query.' % ModelClass._meta.object_name)
```
