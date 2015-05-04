LdcBunnyMultiConsumer
=============

---
[![Latest Stable Version](https://poser.pugx.org/adamlundrigan/ldc-bunny-multi-consumer/v/stable.svg)](https://packagist.org/packages/adamlundrigan/ldc-bunny-multi-consumer) [![Total Downloads](https://poser.pugx.org/adamlundrigan/ldc-bunny-multi-consumer/downloads.svg)](https://packagist.org/packages/adamlundrigan/ldc-bunny-multi-consumer) [![Latest Unstable Version](https://poser.pugx.org/adamlundrigan/ldc-bunny-multi-consumer/v/unstable.svg)](https://packagist.org/packages/adamlundrigan/ldc-bunny-multi-consumer) [![License](https://poser.pugx.org/adamlundrigan/ldc-bunny-multi-consumer/license.svg)](https://packagist.org/packages/adamlundrigan/ldc-bunny-multi-consumer)
[![Build Status](https://travis-ci.org/adamlundrigan/LdcBunnyMultiConsumer.svg?branch=master)](https://travis-ci.org/adamlundrigan/LdcBunnyMultiConsumer)
[![Code Coverage](https://scrutinizer-ci.com/g/adamlundrigan/LdcBunnyMultiConsumer/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/adamlundrigan/LdcBunnyMultiConsumer/?branch=master)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/adamlundrigan/LdcBunnyMultiConsumer/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/adamlundrigan/LdcBunnyMultiConsumer/?branch=master)

---

## What?

It's a simple helper class to make setting up asynchronous AMQP consumers easy-peasy.  Under the hood it uses [Bunny](https://github.com/jakubkulhan/bunny)'s async AMQP client.

## How?

1. Install the [Composer](https://getcomposer.org/) package:

    ```
    composer require adamlundrigan/ldc-bunny-multi-consumer:1.*@stable
    ```

2. Create a consumer:

```
<?php

use Bunny\Message;
use Bunny\Channel;
use Bunny\AbstractClient as Client;

require 'vendor/autoload.php';

// You can also pass a Bunny client object
$consumer = new \LdcBunnyMultiConsumer\MultiConsumer([
    'host' => '127.0.01',
    'port' => 5672
]);

$consumer->bind('exchange_one', null, function(Message $m, Channel $c, Client $cl) {
    // @TODO handle message from exchange_one
});

$consumer->bind('exchange_two', 'this_is_a_named_queue', function(Message $m, Channel $c, Client $cl) {
    // @TODO handle message from exchange_two
});

$consumer->run();
```

3. Profit!
