## PersonId

> Short, but more importantly **human-proof** non-sequential url-friendly unique id generator.


PersonId is a clone of [ShortID](https://github.com/dylang/shortid#readme) which is a clone of [nano-id](https://github.com/ai/nanoid). The emphasis is different from both of those projects, and is instead human centric. The characters must be easy to type on a phone. Also there can be no confusion with similar keys. The following letters that might be confusing to someone are:

```
I -> 1
L -> 1
O -> 0
S -> 5
```

So in total the alphabet/dictionary consists in total of 32 bits using:
```
0123456789ABCDEFGHJKMNPQRTUVWXYZ
```

### Usage

```js
const personid = require('personid');

console.log(personid.generate());
// BNPANGQD78C4ZH
```

### Browser Compatibility

The best way to use `personid` in the browser is via [browserify](http://browserify.org/) or [webpack](http://webpack.github.io/).

These tools will automatically only include the files necessary for browser compatibility.

All tests will run in the browser as well:

```bash
## build the bundle, then open Mocha in a browser to see the tests run.
$ grunt build open
```


### API

```js
var personid = require('personid');
```

---------------------------------------

#### `personid.generate()`

__Returns__ `string` non-sequential unique id.

__Example__

```js
users.insert({
  _id: personid.generate(),
  name: '...',
  email: '...'
});
```

#### `personid.isValid(id)`

__Returns__ `boolean`

Check to see if an id is a valid `personid`. Note: This only means the id _could_ have been generated by `personid`, it doesn't guarantee it.

__Example__

```js
personid.isValid('A2CJEHGW879D8X');
// true
```

```js
personid.isValid('i have spaces');
// false
```

---------------------------------------

#### `personid.worker(integer)`

__Default:__ `process.env.NODE_UNIQUE_ID || 0`

__Recommendation:__ You typically won't want to change this.

__Optional__

If you are running multiple server processes then you should make sure every one has a unique `worker` id. Should be an integer between 0 and 16.
If you do not do this there is very little chance of two servers generating the same id, but it is theoretically possible
if both are generated in the exact same second and are generating the same number of ids that second and a half-dozen random numbers are all exactly the same.

__Example__

```js
personid.worker(1);
```

---------------------------------------

#### `personid.seed(integer)`

__Default:__ `1`

__Recommendation:__ You typically won't want to change this.

__Optional__

Choose a unique value that will seed the random number generator so users won't be able to figure out the pattern of the unique ids. Call it just once in your application before using `personid` and always use the same value in your application.

Most developers won't need to use this, it's mainly for testing personid.

If you are worried about users somehow decrypting the id then use it as a secret value for increased encryption.

__Example__

```js
personid.seed(1000);
```



### License
Released under the [MIT license](https://tldrlegal.com/license/mit-license).
