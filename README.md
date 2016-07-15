# Node.js Express Middleware

## Objectives

1. Explain what we mean by "middleware"
2. Describe how to use middleware in an Express application
3. Code-along to define simple middleware

## Introduction

Suggestion for a narrative frame: using the elevator in the Empire State Building. You have to get a ticket first

```
curl /ticket
```

Which you need to provide when entering:

```
curl /elevator?ticket={ticket}
```

And you can only get off on certain floors? (I'm not actually sure that's how it works, but let's go with it.)

```
curl /floors/7 // 400
curl /floors/20 // 200
```

Feel free to change that, just a thought.

As for the code, in the abstract:

It might be helpful to start with a simple server with no middleware

``` javascript
const express = require('express');

const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!\n');
});

app.listen(3000, () => {
  console.log('Listening on port 3000');
});
```

(I've added this to `index.js`.)

Have students `curl http://localhost:3000` to get a feel for how this works.

Then, add a simple global middleware:

```
app.use((req, res, next) => {
  if (req.path === '/') {
    return next();
  }

  res.send("Whoa there! Where do you think you're going?");
});
```

And have them try that out: `curl http://localhost:3000/nope`.

Try adding a few examples; make it clear that they can do *anything* in these middleware.

Work up to adding route-specific middleware. This is what we'll want to test in the following lab.

## Resources

- [Express: Writing Middleware](http://expressjs.com/en/guide/writing-middleware.html)
- [Express: Using Middleware](http://expressjs.com/en/guide/using-middleware.html)
