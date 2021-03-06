# The Feathers Philosophy

We know! You're probably screaming _"Not another JavaScript framework!"_. We've also become frustrated with all the Rails clones and MVC frameworks that don't do anything different. Instead, a few years ago we started to explore a different approach to building web applications using services and cross cutting concerns while also being careful not to reinvent the wheel.

With this experimentation Feathers has grown into what it is today. Our core philosophy that guides Feathers is still the same as it was years ago:

> _"Monolithic apps fall apart at scale. What if we could make it easy to build service oriented applications from day one rather than having to start with a large application and go through the painful process of breaking it apart? This is usually a result of inflexible frameworks and technical debt._
>
> _A framework itself should not be opinionated. It should be made up of small, reusable, optional components that do one thing well but are combined in an opinionated way. By keeping the components of your application small, flexible and optional you eliminate much of the engineering obstacles that prevent moving fast and scaling."_

We strongly believe that your UI, data and business logic are the core of any web or mobile application and your framework should take care of the rest so you can focus on the things that matter.

## The services concept

Many web frameworks focus on things like rendering views, defining routes and handling HTTP requests and responses without providing a structure for implementing application logic separate from those secondary concerns. The result - even when using the MVC pattern - are monolithic applications with messy controllers or fat models. Your actual application logic and how your data is accessed are all mixed up together.

Feathers brings 3 important concepts together that help to separate those concerns from how your application works and give you incredible flexibility while still keeping things [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself).

#### Services

A service layer which helps to decouple your application logic from how it is being accessed and represented. Besides also making things a lot easier to test - you just call your service methods instead of having to make fake HTTP requests - this is what allows Feathers to provide the same API through both HTTP REST and websockets. It can even be extended to use any other RPC protocol and you won't have to change any of your services.

#### Uniform Interfaces

Every Feathers service exposes a uniform interface modeled after REST. Where, just like one of the key constraints of REST, your action context is immediately apparent due to the naming convention. With REST you have the HTTP verbs (GET, POST, PUT, PATCH and DELETE). This translates naturally to a Feathers service object interface:

```js
const myService = {
  // GET /path
  find(params, callback) {},
  // GET /path/<id>
  get(id, params, callback) {},
  // POST /path
  create(data, params, callback) {},
  // POST /path/<id>
  update(id, data, params, callback) {},
  // PATCH /path/<id>
  patch(id, data, params, callback) {},
  // DELETE /path/<id>
  remove(id, params, callback) {}
}
```

This interface also makes it easier to "hook" into the execution of those methods and emit events when they return which can naturally be used to provide real-time functionality.

#### Hooks

[Cross cutting concerns](https://en.wikipedia.org/wiki/Cross-cutting_concern) are an extremely powerful part of aspect oriented programming. They are a very good fit for web and mobile applications since the majority are primarily CRUD applications with lots of shared functionality. Keeping with the Unix philosophy we believe that small modules that do one thing are better than large complex ones. That's why you can create `before` and `after` hooks and chain them together to create very complex processes while still maintaining modularity and flexibility.

## Built on the Shoulders of Giants
Because we utilize some already proven modules, we spend less time re-inventing the wheel, are able to move incredibly fast, and have small well-tested, stable modules.

Here's how we use some of the tech under the hood:

- Feathers extends [Express 4](http://expressjs.com), the most popular web framework for [NodeJS](http://nodejs.org/).
- Our CLI tool extends [Vorpal](http://vorpal.js.org), its generators are built with [Yeoman](http://yeoman.io/).
- We wrap [Socket.io](http://socket.io/) or [Primus](https://github.com/primus/primus) as your websocket transport.
- Our service adapters typically wrap mature ORMs like [mongoose](http://mongoosejs.com/), [sequelize](http://docs.sequelizejs.com/), [knex](http://knexjs.org/), or [waterline](https://github.com/balderdashy/waterline).
- [npm](http://npmjs.org) for package management.
- [passport](http://passportjs.org/) for much of the [feathers-authentication](https://github.com/feathersjs/feathers-authentication) work.

Now that you know a bit about where Feathers comes from [let's look at what Feathers provides](features.md).
