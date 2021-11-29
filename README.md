# Simple PHP Amazon scraper
This library is a Guzzle-based wrapper around RapidAPI solution which scrapes Amazon product details and reviews.

Get your access key here:
https://rapidapi.com/restyler/api/amazon23

See /examples folder for examples

## Installation
```
composer require restyler/amazon-scraper
```

## Quick example:
### getProductDetails(): Get product details by ASIN
```php
use AmazonScraper\Client;

$amazonClient = new Client([
        'rapidapi_key' => 'YOUR-RAPID-API_KEY'
    ]
);

$response = $amazonClient->getProductDetails([
    'asin' => 'B07XQXZXJC',
    'country' => 'US'
]);

print_r($response);

```


## Proxy Support
This RapidAPI API uses a network of proxies so you don't need to manage proxies manually.

## Examples, Error Handling
See full example file [here](examples/index.php).


