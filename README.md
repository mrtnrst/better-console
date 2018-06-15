# better-console

_DISCLAIMER: This project is exactly as the good console with one extra feature, passing payloads into the console._

`good-console` is a transform stream useful for turning [good](https://github.com/hapijs/good) server events into formatted strings.

[![Build Status](https://travis-ci.org/mrtnrst/better-console.svg?branch=master)](https://travis-ci.org/mrtnrst/better-console)
[![Current Version](https://img.shields.io/npm/v/good-console.svg)](https://www.npmjs.com/package/a-better-console)

Lead Maintainer: [Martin Arista](https://github.com/mrtnrst)

## Usage

## `new GoodConsole([config])`
Creates a new GoodConsole object with the following arguments:

- `[config]` - optional configuration object with the following keys
	- `format` - [MomentJS](http://momentjs.com/docs/#/displaying/format/) format string. Defaults to 'YYMMDD/HHmmss.SSS'.
	- `utc` - boolean controlling Moment using [utc mode](http://momentjs.com/docs/#/parsing/utc/) or not. Defaults to `true`.
	- `color` - a boolean specifying whether to output in color. Defaults to `true`.
	- `requestPayload` a boolean specifying if passed request payload will be output to console. Defaults to `false`.
	- `responsePayload` a boolean specifying if passed response payload will be output to console. Defaults to `false`.

## Output Formats

Below are example outputs for the designated event type:

- "ops" - 160318/013330.957, [ops] memory: 29Mb, uptime (seconds): 6, load: [1.650390625,1.6162109375,1.65234375]
- "error" - 160318/013330.957, [error,`event.tags`] message: Just a simple error, stack: `event.error.stack`
- "request" - 160318/013330.957, [request,`event.tags`] data: you made a request
- "log" - 160318/013330.957, [log,`event.tags`] data: you made a default
- "response" - 160318/013330.957, [response, `event.tags`] http://localhost:61253: post /data {"name":"adam"} 200 (150ms)


## Example
```js
const Logging = {
    register: require('good'),
    options: {
        reporters: {
            console: [{
                module: 'good-squeeze',
                name: 'Squeeze',
                args: [{
                    log: '*',
                    request: '*',
                    error: '*',
                }],
            }, {
                module: 'good-console',
                args: [{
                    responsePayload: true,
                }],
            }, 'stdout'],
        },
        includes: {
            request: ['payload'],
            response: ['payload'],
        },
    },
};
```
