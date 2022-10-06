# Session handling by scoped_session

tags: #python #sqlalchemy #database

While using SqlAlchemy, remember how the sessions are managed by the sessionmaker.
`scoped_session` returns a [registry](https://martinfowler.com/eaaCatalog/registry.html)

- It can be used directly or we can get an available session through it
- It handles creating a session if none is available

```py 
from sqlalchemy.orm import sessionmaker, scoped_session

sharded_session = sessionmaker(query_cls=CustomQuery, class_=ShardedSession)
session = scoped_session(sharded_session) 
```

This `session` should be more like `session_registry`, althought its not
because you can use it directly, which has been misleading in the past.

For the sake of the example, let's assume it's called `session_registry`

You can either do:

```py
session_registry.query(SomeClass) 
```

or

```py
session = session_registry()
session.query(SomeClass) 
```

The end result is the same, but the first one hides the fact that it creates
the session and keeps it available for further use within the registry

Now, the first one I think can be more explicit about cleaning up. Using the
registry directly often end up meaning letting the underlying API framework
handling the removal. Something like

```py
@on_request_end
def remove_session(req):
    session_registry.remove()
```

When can this be a problem?

- Handling multiple DB connections as the engine used is set when creating the session
- ¯\_(ツ)_/¯ Haven't found any other cases, unless you are actually fighting against SqlAlchemy's docs

[docs](https://docs.sqlalchemy.org/en/14/orm/contextual.html#using-thread-local-scope-with-web-applications)

----------------------------------------------------------------------
