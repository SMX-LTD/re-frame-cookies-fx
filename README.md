# Cookies Effects Handler for re-frame

> Om Nom Nom Nom - Cookie Monster, Sesame Street

Herein a re-frame ["Effects Handler"](https://github.com/Day8/re-frame/wiki/Effectful-Event-Handlers),
which enables various [cookie](https://en.wikipedia.org/wiki/HTTP_cookie)
operations using [goog.net.Cookies](http://google.github.io/closure-library/api/goog.net.Cookies.html).

## Quick Start

### 1. Add Dependency

[![Clojars Project](https://img.shields.io/clojars/v/com.smxemail/re-frame-cookie-fx.svg)](https://clojars.org/com.smxemail/re-frame-cookie-fx)

### 2. Registration & Use

_Note: Due to recent breaking changes to ClojureScript 1.9's use of spec, version 0.0.2 of this library requires that you use ClojureScript 1.9.542 or later_

In the namespace where you register your event handlers, prehaps called
`handlers.cljs`, you have two things to do:

First, add this `require` to the `ns`:
```clj
(ns app.handlers
  (:require
    ...
    [com.smxemail.re-frame-cookie-fx]    ;; <-- add this
    ...))
```

#### Event handlers

Second, write an event handler which uses this effect:
```clj
(reg-event-fx
  :handler-with-cookies
  (fn [{:keys [db]} _]
    {:cookie/set {:name "cookie-monster-says"
                  :value "Om Nom Nom Nom!"}}))
```

Other supported effects include the below which are documented in the source:
- `:cookie/remove`
- `:cookie/clear`

Besides `:name` and `:value`, you can supply `:on-success` and `:on-failure` handlers as
well as the usual cookie options including `:max-age`, `:path`, `:domain`, and
`:secure`. See details and documentation in the source.

Note that if you do not supply `:on-success` or `:on-failure` to `:cookie/set` or
`:cookie/remove`, the code will default to dispatching to handlers
`:cookie-set-no-on-success`, `:cookie-set-no-on-failure`,
`:cookie-remove-no-on-success`, and `:cookie-remove-no-on-failure`. You must supply
these event handlers.


#### Coeffects

To use a coeffect:
```clj
(reg-event-fx
  :handler-with-cookie-cofx
  [(inject-cofx :cookie/get [:cookie-monster-says])]
  (fn [{db :db cookies :cookie/get} _]
        ...
```

Other supported coeffects include the below which are documented in the source:
- `:cookie/enabled?`
- `:cookie/empty?`
- `:cookie/keys`
- `:cookie/values`
- `:cookie/count`

## Authors

- [Isaac Johnston](@superstructor)
- [Abhishek Reddy](@arbscht)

## License

Copyright &copy; 2016 SMX Ltd.

Distributed under the Eclipse Public License, the same as Clojure.
