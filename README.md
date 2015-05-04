LdcBunnyMultiConsumer
=============

---
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

