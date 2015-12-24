---
layout: post
title:  "React-Router"
date:   2015-12-23 13:35:30
categories: allen.hu update
---

# React-Router

A complete routing solution for React.js

## Docs

###Intodrucitons

* Without React Router

* With React Router

* Add more UI

###Basics

####Route Configuration

* Adding an Index
* Decoupling the UI from the URL
* Preserving URLs Redirect from... to...
* Enter and Leave Hooks
* Alternate Configuration


IndexRoute  This functionality is similar to Apaches's DirectoryIndex or nginx's index directive.

#### Route Matching

A route has three attibutes that determine wheter or not it "matches" the URL:

1. nesting and
2. its path
3. its precedence

* :paramName – matches a URL segment up to the next /, ?, or #. The matched string is called a param
* () – Wraps a portion of the URL that is optional
* * – Matches all characters (non-greedy) up to the next character in the pattern, or to the end of the URL if there is none, and creates a splat param
* ** - Matches all characters (greedy) until the next /, ?, or # and creates a splat param

<Route path="/hello/:name">         // matches /hello/michael and /hello/ryan
<Route path="/hello(/:name)">       // matches /hello, /hello/michael, and /hello/ryan
<Route path="/files/*.*">           // matches /files/hello.jpg and /files/hello.html
<Route path="/**/*.jpg">            // matches /files/hello.jpg and /files/path/to/file.jpg

#### Histories

There are three types of histories you'll come across most often. but note that anyone can build a custom history implementation for consumption with React Router.

1. createHashHistory
This is the default history your'll get if you don't specify a history at all.

2. createBrowserHistory
Hash history and works in all evergreen browsers and IE8+, but, we don't recommend using it in production. every web ap should aspire to use createBrowserHistory.

3. createMemoryHistory

It's also useful for testing and other rendering environments(like React Native)




#### Index Routes and Links

To illustrate the use case for IndexRoute, imagine the following route config without it:

```
<Router>
  <Route path="/" component={App}>
    <Route path="accounts" component={Accounts}/>
    <Route path="statements" component={Statements}/>
  </Route>
</Router>

When teh user visits /, the App component is rendered ,but none of the children are, so this.props.children inside of App will be undefined, To render some default UI you c olud easyliy to
{this.props.children||<HOME/>}

But now Home can't  participate in routing , like the  onEnter hooks, etc. You render in the same position as Accounts and Statement, so the router allows your to hae Home be a  first class route component  with IndexRoute.

```
<Router>
  <Route path="/" component={App}>
    <IndexRoute component={Home}/>
    <Route path="accounts" component={Accounts}/>
    <Route path="statements" component={Statements}/>
  </Route>
</Router>

Now App can render {this.props.children} and we have a first-class route for Home that can  participate in routing.



###Advanced Usage

####Dynamic Routing

A router is the  perfect place to handle code splitting:  it's responsible for setting up your views.

Routes may define getChildroutes, getIndexRoute, and getComponents methods. These are asynchronous and only called when needed, We call it "gradual matching", React Route
will gradually match the URL and fetch only the amount of route configuration and components it needs to match the URL and render.

Look example huge apps of the react-router examples directory.


####Confirming Navigation

React Router provides a routerWillLeave lifecycle hook that React components may use to prevent a transition from happening or to prompt the user before leaving a route. routerWillLeave may either.

```
import { Lifecycle, RouteContext } from 'react-router'

const Home = React.createClass({

  // Home should provide its route in context
  // for descendants further down the hierarchy.
  mixins: [ RouteContext ],

  render() {
    return <NestedForm />
  }

})

const NestedForm = React.createClass({

  // Descendants use the Lifecycle mixin to get
  // a routerWillLeave method.
  mixins: [ Lifecycle ],

  routerWillLeave(nextLocation) {
    if (!this.state.isSaved)
      return 'Your work is not saved! Are you sure you want to leave?'
  },

  // ...

})


####Server Rendering

500
400
302

####Component Lifecycle

* Lifecycle hooks when routing.
*

####Navigating Outside of Components
While route components get this.props.history and the History mixin provides this.history, many apps want to be able to navigate outside of their components.


## API Reference
###Commponents

* Router
stringifyQuery, parseQueryString

* Link
* IndexLink
* RouterContext

### Configuration Components

* IndexRoute
Index Routes allow you to provide a default "child" to a parent route when visitor is at the URL of the parent, they provide convention for <IndexLInk> to work.


## React Router Examples

1. clone [React-Router](https://github.com/rackt/react-router.git)
2. run npm install
3. npm start
4. http://localhost:8080

abundance case

* active-links

```
render((
  <Router history={browserHistory}>
    <Route path="/" component={App}>
      <IndexRoute component={Index}/>
      <Route path="/about" component={About}/>
      <Route path="users" component={Users}>
        <IndexRoute component={UsersIndex}/>
        <Route path=":id" component={User}/>
      </Route>
    </Route>
  </Router>
), document.getElementById('example'))


* animations
```
<ReactCSSTransitionGroup
          component="div"
          transitionName="example"
          transitionEnterTimeout={500}
          transitionLeaveTimeout={500}
        >
	  {React.cloneElement(this.props.children, {
	    key: this.props.location.pathname
	  })}
</ReactCSSTransitionGroup>

* auth-flow
```
module.exports = {
  login(email, pass, cb) {
    cb = arguments[arguments.length - 1]
    if (localStorage.token) {
      if (cb) cb(true)
      this.onChange(true)
      return
    }
    pretendRequest(email, pass, (res) => {
      if (res.authenticated) {
        localStorage.token = res.token
        if (cb) cb(true)
        this.onChange(true)
      } else {
        if (cb) cb(false)
        this.onChange(false)
      }
    })
  },

  getToken() {
    return localStorage.token
  },

  logout(cb) {
    delete localStorage.token
    if (cb) cb()
    this.onChange(false)
  },

  loggedIn() {
    return !!localStorage.token
  },

  onChange() {}
}

function pretendRequest(email, pass, cb) {
  setTimeout(() => {
    if (email === 'joe@example.com' && pass === 'password1') {
      cb({
        authenticated: true,
        token: Math.random().toString(36).substring(7)
      })
    } else {
      cb({ authenticated: false })
    }
  }, 0)
}


* auth-with-shared-root

route config

* dynamic-segments

```
class Task extends React.Component {
  render() {
    const { userID, taskID } = this.props.params

    return (
      <div className="Task">
        <h2>User ID: {userID}</h2>
        <h3>Task ID: {taskID}</h3>
      </div>
    )
  }
}

render((
  <Router history={browserHistory}>
    <Route path="/" component={App}>
      <Route path="user/:userID" component={User}>
        <Route path="tasks/:taskID" component={Task} />
        <Redirect from="todos/:taskID" to="tasks/:taskID" />
      </Route>
    </Route>
  </Router>
), document.getElementById('example'))

* master-detail

ContactStore

* nested-animations

```
<ReactCSSTransitionGroup
      component="div" transitionName="swap"
      transitionEnterTimeout={500} transitionLeaveTimeout={500}
    >
      {React.cloneElement(this.props.children || <div />, { key: key })}
</ReactCSSTransitionGroup>

* passing-props-to-children

```
 <div className="Detail">
          {this.props.children && React.cloneElement(this.props.children, {
            onRemoveTaco: this.handleRemoveTaco
          })}
