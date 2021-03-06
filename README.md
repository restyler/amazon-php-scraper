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
        'rapidapi_key' => 'YOUR-RAPIDAPI-KEY'
    ]
);

$response = $amazonClient->getProductDetails([
    'asin' => 'B07XQXZXJC',
    'country' => 'US'
]);

echo json_encode($response);
/*
response will contain:
{
  "result": [
    {
      "title": "TCL 10 SE Unlocked Android Smartphone, 6.52\" V-Notch Display, US Version Cell Phone with 16 MP Rear AI Triple-Camera 4GB RAM + 64GB ROM, 4000mAh Fast Charging Battery, ICY Silver",
      "description": "",
      "feature_bullets": [
        "Large Storage Space & Wireless Carrier: The octa-co...)",
        "Enjoy An Unbeatable Visual Experience: .."
      ],
      "variants": [
        {
          "asin": "B09295KQ9Q",
          "images": [
            "https://m.media-amazon.com/images/I/417ta4WBBCL._AC_SY879_.jpg"
          ],
          "title": "Icy Silver",
          "link": "https://www.amazon.com/dp/B09295KQ9Q/?th=1&psc=1",
          "is_current_product": true,
          "price": " $179.99 "
        },
        {
          "asin": "B09295GRFS",
          "images": [
            "https://m.media-amazon.com/images/I/41z-UqtAk2L._AC_SY879_.jpg"
          ],
          "title": "Polar Night",
          "link": "https://www.amazon.com/dp/B09295GRFS/?th=1&psc=1",
          "is_current_product": false,
          "price": " $179.99 "
        }
      ],
      "categories": [
        {
          "category": "Cell Phones & Accessories",
          "url": "https://www.amazon.com/cell-phones-service-plans-accessories/b/ref=dp_bc_aui_C_1/137-5978987-1987860?ie=UTF8&node=2335752011"
        },
        {
          "category": "Cell Phones",
          "url": "https://www.amazon.com/cell-phone-devices/b/ref=dp_bc_aui_C_2/137-5978987-1987860?ie=UTF8&node=7072561011"
        }
      ],
      "asin": "B09295KQ9Q",
      "url": "https://www.amazon.com/dp/B09295KQ9Q",
      "reviews": {
        "total_reviews": 896,
        "rating": "4.2",
        "answered_questions": 316
      },
      "item_available": true,
      "price": {
        "symbol": "$",
        "currency": "USD",
        "current_price": 179.99,
        "discounted": false,
        "before_price": 179.99,
        "savings_amount": 0,
        "savings_percent": 0
      },
      "bestsellers_rank": [],
      "main_image": "https://m.media-amazon.com/images/I/417ta4WBBCL._AC_SY879_.jpg",
      "total_images": 7,
      "images": [
        "https://m.media-amazon.com/images/I/417ta4WBBCL._AC_SY879_.jpg",
        "https://m.media-amazon.com/images/I/31hq98Yx5FL._AC_SY879_.jpg",
        "https://m.media-amazon.com/images/I/316nZ6EyghL._AC_SY879_.jpg",
        "https://m.media-amazon.com/images/I/41M5n-JvieL._AC_SY879_.jpg",
        "https://m.media-amazon.com/images/I/41AQr0dNd5L._AC_SY879_.jpg",
        "https://m.media-amazon.com/images/I/41YKElUy73L._AC_SY879_.jpg",
        "https://m.media-amazon.com/images/I/41MUreBA8QL._AC_SY879_.jpg"
      ],
      "total_videos": 0,
      "videos": [],
      "delivery_message": "",
      "product_information": {
        "dimensions": "",
        "weight": "",
        "available_from": "",
        "available_from_utc": "",
        "available_for_months": 0,
        "available_for_days": 0,
        "manufacturer": "",
        "model_number": "",
        "department": "",
        "qty_per_order": 5,
        "store_id": "",
        "brand": "Visit the TCL Store"
      },
      "badges": { "amazon_\u0441hoice": true, "amazon_prime": false },
      "sponsored_products": [],
      "also_bought": [],
      "other_sellers": []
    }
  ]
}

*/

```

### getProductReviews(): Get product reviews by ASIN
```php
use AmazonScraper\Client;

$amazonClient = new Client([
        'rapidapi_key' => 'YOUR-RAPIDAPI-KEY'
    ]
);

$response = $amazonClient->getProductReviews([
    'asin' => 'B07XQXZXJC',
    'country' => 'US',
    'page' => 1, // pagination starts from page#1
    'sort_by' => 'recent' // 'recent' or 'helpful'
]);

echo json_encode($response);

/*
response will contain:
{
  "total_reviews": 897,
  "stars_stat": { "1": "8%", "2": "4%", "3": "7%", "4": "17%", "5": "63%" },
  "result": [
    {
      "id": "R2BHM8R45IZZWS",
      "asin": { "original": "B09295KQ9Q", "variant": "B09295GRFS" },
      "review_data": "Reviewed in the United States on November 26, 2021",
      "date": { "date": "November 26, 2021", "unix": 1637892000 },
      "name": "Thomas Murcko",
      "rating": 1,
      "title": "Low quality phone",
      "review": "The software on the phone is like something from 2008. Terrible phone if you need apps and browsing to function with out 5 second delays and freezing, oh and not doing what you need it to. Like loading apps or closing apps. Waste of money",
      "verified_purchase": false
    },
    {
      "id": "R186NHV1T171NC",
      "asin": { "original": "B09295KQ9Q", "variant": "B09295GRFS" },
      "review_data": "Reviewed in the United States on November 26, 2021",
      "date": { "date": "November 26, 2021", "unix": 1637892000 },
      "name": "Amazon Customer",
      "rating": 5,
      "title": "Best cheap phone I've owned.",
      "review": "Nice cheap phone. Appears faster than it really is. High quality. Only one slight negative. It doesn't have wifi 5g. It does have 2.4g.",
      "verified_purchase": true
    },
    {
      "id": "RRN0QRM0NHHNP",
      "asin": { "original": "B09295KQ9Q", "variant": "B09295GRFS" },
      "review_data": "Reviewed in the United States on November 24, 2021",
      "date": { "date": "November 24, 2021", "unix": 1637719200 },
      "name": "l.johns",
      "rating": 5,
      "title": "Nice phone at a great price.",
      "review": "The package arrived on time.So far, the phone works and it seems to be a nice phone.Also, got it at a great price.",
      "verified_purchase": true
    },
    {
      "id": "R1N9QQQEWZ57WT",
      "asin": { "original": "B09295KQ9Q", "variant": "B09295GRFS" },
      "review_data": "Reviewed in the United States on November 4, 2021",
      "date": { "date": "November 4, 2021", "unix": 1635991200 },
      "name": "SM",
      "rating": 3,
      "title": "Not as fast as my tcl10l",
      "review": "I had my other TCL phone for about 6 months and it had an accident cracking the screen so I got this one as a quick replacement. I've had it for 3 days I'm not thrilled with it the apps on it have a lot of trouble when I'm out in public and not on Wi-Fi. My old TCL worked a lot faster as far as running apps or doing a Google search or something like that on the cellular data even though they were both unlocked phones this one just doesn't seem to have as great of a reception as the other one did. Picture quality on this phone and the other TCL are wonderful and definitely some of the best picture quality for the price.",
      "verified_purchase": true
    }
  ]
}

*/

```

### searchProducts(): Search products by keyword
```php
use AmazonScraper\Client;

$amazonClient = new Client([
        'rapidapi_key' => 'YOUR-RAPIDAPI-KEY'
    ]
);

$response = $amazonClient->searchProducts([
    'query' => 'xbox',
    'country' => 'US',
    'page' => 2, // pagination starts from page#1
]);

echo json_encode($response);

/*
response will contain:
{
  "totalProducts": 0,
  "category": "aps",
  "result": [
    {
      "position": { "page": 1, "position": 1, "global_position": 1 },
      "asin": "B09BJ1V35W",
      "price": {
        "discounted": false,
        "current_price": 17.99,
        "currency": "USD",
        "before_price": 0,
        "savings_amount": 0,
        "savings_percent": 0
      },
      "reviews": { "total_reviews": 124, "rating": 4.5 },
      "url": "https://www.amazon.com/dp/B09BJ1V35W",
      "score": "558.00",
      "sponsored": false,
      "amazonChoice": false,
      "bestSeller": false,
      "amazonPrime": false,
      "title": "Sponsored Ad - EooCoo Compatible with MacBook Air 13 inch Case 2021 2020 2019 2018 M1 A2337 A2179 A1932 with Retina Displa...",
      "thumbnail": "https://m.media-amazon.com/images/I/71veZ8Hq-oL._AC_UY218_.jpg"
    },
    {
      "position": { "page": 1, "position": 2, "global_position": 2 },
      "asin": "B08SJSZGB5",
      "price": {
        "discounted": false,
        "current_price": 28.8,
        "currency": "USD",
        "before_price": 0,
        "savings_amount": 0,
        "savings_percent": 0
      },
      "reviews": { "total_reviews": 482, "rating": 4.6 },
      "url": "https://www.amazon.com/dp/B08SJSZGB5",
      "score": "2217.20",
      "sponsored": false,
      "amazonChoice": false,
      "bestSeller": false,
      "amazonPrime": false,
      "title": "Sponsored Ad - Batianda for MacBook Air 13 inch Case A2337 M1 A2179 A1932 (2020 2019 2018 Release) with Touch ID, Heavy Du...",
      "thumbnail": "https://m.media-amazon.com/images/I/61fb3jeOUsL._AC_UY218_.jpg"
    },
    {
      "position": { "page": 1, "position": 3, "global_position": 3 },
      "asin": "B08N5M9XBS",
      "price": {
        "discounted": false,
        "current_price": 0,
        "currency": "USD",
        "before_price": 0,
        "savings_amount": 0,
        "savings_percent": 0
      },
      "reviews": { "total_reviews": 10850, "rating": 4.8 },
      "url": "https://www.amazon.com/dp/B08N5M9XBS",
      "score": "52080.00",
      "sponsored": false,
      "amazonChoice": false,
      "bestSeller": false,
      "amazonPrime": false,
      "title": "2020 Apple MacBook Air Laptop: Apple M1 Chip, 13\u201d Retina Display, 8GB RAM, 512GB SSD Storage, Backlit Keyboard, FaceTime H...",
      "thumbnail": "https://m.media-amazon.com/images/I/71vFKBpKakL._AC_UY218_.jpg"
    },
    {
      "position": { "page": 1, "position": 4, "global_position": 4 },
      "asin": "B08YCXXJFV",
      "price": {
        "discounted": false,
        "current_price": 1449,
        "currency": "USD",
        "before_price": 0,
        "savings_amount": 0,
        "savings_percent": 0
      },
      "reviews": { "total_reviews": 11, "rating": 4.3 },
      "url": "https://www.amazon.com/dp/B08YCXXJFV",
      "score": "47.30",
      "sponsored": false,
      "amazonChoice": false,
      "bestSeller": false,
      "amazonPrime": false,
      "title": "Apple MacBook Air 13.3\" with Retina Display, M1 Chip with 8-Core CPU and 8-Core GPU, 16GB Memory, 512GB SSD, Space Gray, L...",
      "thumbnail": "https://m.media-amazon.com/images/I/51cND46Q0VL._AC_UY218_.jpg"
    }
  ]
}

*/

```


## Proxy Support
[This solution uses a network of proxies](https://rapidapi.com/restyler/api/amazon23) so you don't need to manage proxies manually.

## Examples, Error Handling
See full example file [here](examples/index.php).


