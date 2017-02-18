# Errors

Catchall error handling, while better than nothing, often just isn't enough. (There's a big difference between "that is not a valid username" and "we aren't able to create new users at all right now".) In order to negotiate the different kinds of errors appropriately, you'll need to be able to examine them in a granular way.

When using code that interacts with Waterline (usually through model methods) there are a few different kinds of error you may encounter, which are easily distinguished by `name` or `code`.

### Usage error

When an error has `name: 'UsageError'`, this indicates that there was a validation error when attempting to use a Waterline method. This sort of error will include validation info.

### Adapter error

Adapter errors usually indicate a problem in the underlying adapter, and not in the request itself. This can happen when a database goes offline, when there is a permission issue, because of some database-specific edge case, or (more rarely) a bug in the adapter.

The one time an adapter error _is_ the result of a problem with the request is when there is a uniqueness constraint violation.

In the case of problem with the adapter, the error will have `name: 'AdapterError'`.

##### Uniqueness

A uniqueness error occurs when a value that _should_ be unique matches that of another record in the database. While this is considered an adapter error, it has its own `code` to differentiate it from a normal adapter error: `code: 'E_UNIQUE'`.

This sort of error can only occur with `.create()`, `.update()`, `.addToCollection()`, and `.replaceCollection()`.

### Negotiating errors

The exact strategy you use to do this in your Sails app depends on whether you're using [callbacks or promises](https://github.com/balderdashy/sails/issues/3459#issuecomment-171039631).  Remember: use whatever you're most comfortable with.  If you aren't sure, start with callbacks.

##### Negotiating errors with callbacks

To handle the different errors that may occur when attempting to create a new user:

```javascript
User.create({
  email: req.param('email')
})
.exec(function(err){
  if (err){
    // Uniqueness constraint violation
    if (err.code === 'E_UNIQUE') {
      return res.status(401).json(err);
    }
    // Some other kind of usage / validation error
    else if (err.name === 'UsageError') {
      return res.badRequest(err);
    }
    // If something completely unexpected happened.
    else {
      return res.serverError(err);
    }
  }

  return res.ok();
})
```

##### Negotiating errors with promises

To handle the different errors that may occur when attempting to create a new user:

```javascript
User.create({
  email: req.param('email')
})
.then(function (){
  return res.ok();
})
// Uniqueness constraint violation
.catch({ code: 'E_UNIQUE' }, function (err) {
  return res.status(401).json(err);
})
// Some other kind of usage / validation error
.catch({ name: 'UsageError' }, function (err) {
  return res.badRequest(err);
})
// If something completely unexpected happened.
.catch(function (err) {
  return res.serverError(err);
});
```


<docmeta name="displayName" value="Errors">