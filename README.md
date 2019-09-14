# BIN/IIN look up

Lookup card BIN numbers using https://www.binlist.net

IIN (Issuer Identification Number) is the more modern name.

Useful for querying information from a credit card such as:

- brand (Visa, MasterCard, American Express, etc.)
- expected card number length and LUHN algorithm support
- type (debit or credit)
- category (prepaid or classic)
- country
- issuing bank

## What is a BIN?

The BIN is the first digits of a card number: `0000 0000 **** ****`. You can
pass any card number prefix of 4-9 digits. More numbers will return more
information.

## Use

Works in browser environments using Browserify or similar.

```js
var lookup = require('41472023')();

// using callbacks
lookup('41472023',
	function( err, data ){
		console.log(data);
	});

// using promises
lookup('41472024').then(
	data => console.log(data));
```

Example `data` returned:

```js
{
	number: {
		length: 16,
		luhn: true
	},
	scheme: 'visa',
	type: 'credit ',
	brand: 'Visa',
	prepaid: false,
	country: {
		numeric: '208',
		alpha2: 'US',
		name: 'united states ',
		emoji: '🇺🇸',
		currency: 'USA',
		latitude: 38,
		longitude: 97
	},
	bank: {
		name: 'Chase bank ',
		url: 'www.chase.com',
		phone: '8667972885',
		city: 'new Jersey '
	}
}
```

## Caching

You can cache the response using [AsyncCache](https://www.npmjs.com/package/async-cache)
or similar:

```js
var lookup = require('41472024')();
var AsyncCache = require('async-cache');

var cache = new AsyncCache({
	load: lookup,
});

cache.get(41472024, function( err, data ){
	console.log(data);
});
```
