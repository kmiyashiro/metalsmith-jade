# Metalsmith Jade [![version][npm-version]][npm-url] [![License][npm-license]][license-url]

[Metalsmith](http://www.metalsmith.io/) plugin to convert jade files.

[![Build Status][travis-image]][travis-url]
[![Downloads][npm-downloads]][npm-url]
[![Code Climate][codeclimate-quality]][codeclimate-url]
[![Coverage Status][codeclimate-coverage]][codeclimate-url]
[![Dependencies][david-image]][david-url]

## Install

```sh
npm install --save metalsmith-jade
```

## API

Pass `options` to the jade plugin and pass it to Metalsmith with the `use` method:

```js
var Metalsmith = require('metalsmith')
var jade = require('metalsmith-jade')

var metalsmith = new Metalsmith(__dirname)
  .use(jade({
    pretty: false,
    locals: {
      postName: 'good post name'
    }
  }))
```

## CLI

You can also use the plugin with the Metalsmith CLI by adding a key to your `metalsmith.json` file:

```json
{
  "plugins": {
    "metalsmith-jade": {
      "pretty": false
    }
  }
}
```

All options are passed directly to jade. If `options` has a `locals` key, that will be passed along to jade.

## Options:

| Name          | Details                                                   | Default |
| ------------- | --------------------------------------------------------- | ------- |
| `useMetadata` | Expose Metalsmith's global metadata to the Jade template. | `false` |
| `pretty`      | If you want pretty HTML or compact HTML.                  | `false` |
| `locals`      | Pass additional variables to the template.                | `{}`    |

### Register a jade filter

Since `metalsmith-jade` uses the jade runtime located at `./node_modules/metalsmith-jade/node_modules/jade` and not the project specific one at `./node_modules/jade` it is not possible to register filters on jade directly.

Therefore the `regiserFilter` method was introduced. The method accepts the name of a filter and a filter factory method. The filter factory method is passed the jade object, the jade runtime *`jade/lib/runtime`* and the jade filters *`jade/lib/filters`*.

it should return a method which will be registered as a jade filter using the name passed as the first argument to the `registerFilter` method.

###### Example

```js
var jade = require('metalsmith-jade');

jade.registerFilter('sample', function (jade, runtime, filters) {
  return function (text) {
    // e.g. convert jade markup to html
    var html = jade.render(text, options)

    // e.g. apply some other jade filter
    var filtered = filters('fooFilter', text)

    // return the markup to be placed at the filter invocations position
    return 'foobar'
  }  
})
```

## Support

Donations are welcome to help support the continuous development of this project.

[![Gratipay][gratipay-image]][gratipay-url]
[![PayPal][paypal-image]][paypal-url]
[![Flattr][flattr-image]][flattr-url]
[![Bitcoin][bitcoin-image]][bitcoin-url]

## License

[MIT](LICENSE) &copy; [Max Bareiss](https://github.com/MaxBareiss), [Ahmad Nassri](https://www.ahmadnassri.com)

[license-url]: https://github.com/ahmadnassri/metalsmith-jade/blob/master/LICENSE

[travis-url]: https://travis-ci.org/ahmadnassri/metalsmith-jade
[travis-image]: https://img.shields.io/travis/ahmadnassri/metalsmith-jade.svg?style=flat-square

[npm-url]: https://www.npmjs.com/package/metalsmith-jade
[npm-license]: https://img.shields.io/npm/l/metalsmith-jade.svg?style=flat-square
[npm-version]: https://img.shields.io/npm/v/metalsmith-jade.svg?style=flat-square
[npm-downloads]: https://img.shields.io/npm/dm/metalsmith-jade.svg?style=flat-square

[codeclimate-url]: https://codeclimate.com/github/ahmadnassri/metalsmith-jade
[codeclimate-quality]: https://img.shields.io/codeclimate/github/ahmadnassri/metalsmith-jade.svg?style=flat-square
[codeclimate-coverage]: https://img.shields.io/codeclimate/coverage/github/ahmadnassri/metalsmith-jade.svg?style=flat-square

[david-url]: https://david-dm.org/ahmadnassri/metalsmith-jade
[david-image]: https://img.shields.io/david/ahmadnassri/metalsmith-jade.svg?style=flat-square

[gratipay-url]: https://www.gratipay.com/ahmadnassri/
[gratipay-image]: https://img.shields.io/gratipay/ahmadnassri.svg?style=flat-square

[paypal-url]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UJ2B2BTK9VLRS&on0=project&os0=metalsmith-jade
[paypal-image]: http://img.shields.io/badge/paypal-donate-green.svg?style=flat-square

[flattr-url]: https://flattr.com/submit/auto?user_id=codeinchaos&url=https://github.com/ahmadnassri/metalsmith-jade&title=metalsmith-jade&language=&tags=github&category=software
[flattr-image]: http://img.shields.io/badge/flattr-donate-green.svg?style=flat-square

[bitcoin-image]: http://img.shields.io/badge/bitcoin-1Nb46sZRVG3or7pNaDjthcGJpWhvoPpCxy-green.svg?style=flat-square
[bitcoin-url]: https://www.coinbase.com/checkouts/ae383ae6bb931a2fa5ad11cec115191e?name=metalsmith-jade
