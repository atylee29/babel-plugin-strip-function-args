# babel-plugin-strip-function-args

Cloned from https://github.com/azu/babel-plugin-strip-function-call and modified to strip args instead.

Strip the specified functions of its parameters.
Useful for removing information to make reverse-engineering more difficult, but 
where the function call must be kept to preserve syntax correctness.

Example: 
```
// Original
const IS_DEBUG = false;
IS_DEBUG && console.log("Checking credentials..."); 

// Args stripped
const IS_DEBUG = false;
IS_DEBUG && console.log();
```

## Install

Install with [npm](https://www.npmjs.com/):

    npm install @atylee29/babel-plugin-strip-function-args --save-dev

## Usage


Via `.babelrc`

```json
{
  "plugins": [
    ["strip-function-args", {
        "strip": [
            "console.log"
        ]
    }]
  ]
}
```

In production only:

```json
{
  "presets": [
    "es2015"
  ],
  "env": {
    "production": {
        "plugins": [
            ["strip-function-args", {
                "strip": [
                    "console.log"
                ]
            }]
        ]
    }
  }
}
```

## Options

- `strip`: `string[]`
    - specify to strip function names

For example, want to strip `console.log(...)`.
Write following:

```js
["strip-function-args", {
    "strip": [
        // not include ()
        "console.log"
    ]
}]
```

### Notes

```js
["strip-function-args", {
    "strip": [
        // not include ()
        "console.log"
    ]
}]
```

The pattern don't strip `console["log"](...)` by design.
If you want to strip computed method pattern, please file issue.


## Changelog

See [Releases page](https://github.com/atylee29/babel-plugin-strip-function-args/releases).

## Running tests

Install devDependencies and Run `npm test`:

    npm i -d && npm test

## Contributing

Pull requests and stars are always welcome.

For bugs and feature requests, [please create an issue](https://github.com/atylee29/babel-plugin-strip-function-args/issues).

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## Author
- [github/azu](https://github.com/atylee29)

## License
MIT ©
