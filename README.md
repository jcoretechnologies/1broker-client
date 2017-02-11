1Broker-client
===

####This is a node.js wrapper for [1Broker's API](https://1broker.com/?c=en/action/r&i=11468), this package is mainly used and maintaned by [@telebroker_bot](https://telegram.me/telebroker_bot) an incredible bot to open orders and manage trades directly from [Telegram](https://telegram.org/) !!!

####Join us at [1Broker Trollbox](https://telegram.me/Trollbox_1Broker) for some trades and trolling, feel free to use the group to ask anything about the Telegram bot as well!
--


This library implements all [1Broker API](https://1broker.com/?c=api_documentation) methods and also a couple extra features:

 - % Stop Loss and Take Profit when creating Market or Limit orders.
 - Option to use "MAX", "HALF" or "QUARTER" as leverage, so it will dynamically adjust based on market MAX leverage.
 - Market information is cached on [details.json](https://github.com/flyingunicorn222/1broker-client/blob/v2/src/info/details.json) allowing quick and smart calculations, for instance:
   - How many points you making in your position?
     - see [client.get.points( symbol, entry, current_price )](https://github.com/flyingunicorn222/1broker-client/blob/v2/src/helpers/get/points.coffee)
   - At what value will a reach that many points?
     - see [client.add.points( symbol, value, points )](https://github.com/flyingunicorn222/1broker-client/blob/v2/src/helpers/add/points.coffee)
   - How many percent a given difference represents with a given leverage?
     - see [client.get.percentage( entry, difference, leverage )](https://github.com/flyingunicorn222/1broker-client/blob/v2/src/helpers/get/percentage.coffee)

Telegram bot
====
All this functionality from this library is available through [@telebroker_bot](https://telegram.me/telebroker_bot) for Telegram, this way you don't have to run commands from your command line and similars, using the bot you get some sort of API REPL which is a lot of fun!

I also created a [Thread on reddit](https://www.reddit.com/r/1Broker/comments/582eks/you_can_buy_and_sell_on_1broker_directly_from/) to speak about it, i'll hopefully keep improving the bot and keeping reddit up to date with the features.

Feel free to contact me there or [open a new issue](https://github.com/flyingunicorn222/1broker-client/issues/new)!


Installing
====

````npm install --save 1broker-client````

Unfortunately new versions might break backwards
compatibility so please make sure you specify a version on your package.json
file.

basics
====

All functions take "callback" as last parameter:

````javascript
OneBroker = require( "1broker-client" )

client = OneBroker( "YOU_API_KEY" )

client.user.overview( function( error, overview ) {
  if( error ) return console.error( error );

  console.log( overview );
} );
````

Functions which need parameters will take them as object, for instance:

````javascript

client.market.quotes({
  symbols: "BTCUSD,GOLD"
}, function( error, quotes ) {
  console.log( quotes );
});

````

Most methods from the API V2 have been implemented


````javascript
client.user.details( callback )
client.user.overview( callback )
client.user.bitcoin_deposit_address( callback )
client.user.transaction_log( params, callback )
client.user.quota_status( callback )

client.order.cancel( params, callback )
client.order.create( params, callback )
client.order.open( callback )

client.position.open( callback )
client.position.edit( params, callback )
client.position.close( params, callback )
client.position.close_cancel( params, callback )
client.position.history( params, callback )

client.market.categories( callback )
client.market.list( params, callback )
client.market.details( params, callback )
client.market.quotes( params, callback )
client.market.bars( params, callback )
client.market.ticks( params, callback )

````

For full [API documentation](https://1broker.com/?c=en/content/api-documentation) please refer to the [Official API](https://1broker.com/?c=en/content/api-documentation)

examples
====

Simple examples are provided on the [/examples](https://github.com/flyingunicorn222/1broker-client/tree/v1/examples) folder, including
the % Stop Loss and Take Profit syntax.

Before running the examples you will need:

 - [1broker Account](https://1broker.com/?c=en/action/r&i=11468)

 - Api Token ( Create one in [Settings](https://1broker.com/?u1=account_settings) )

 - [Coffee-Script](http://coffeescript.org/) ```npm install coffee-script --global```

 - Download the example files

```bash
$ git clone https://github.com/flyingunicorn222/1broker-client.git
$ cd 1broker-client/
$ npm install
$ cd examples
```

 - Edit [.env file](https://github.com/flyingunicorn222/1broker-client/blob/v1/.env) and update with your key

```bash
# .env
KEY=Ac17f4de5...................b69a
```

Now you can run examples, for instance:
```bash
$coffee long_eurusd.coffee
```
or
```bash
$coffee short_btcusd.coffee
```
Examples source code is pretty simple, please [go ahead](https://github.com/flyingunicorn222/1broker-client/blob/v1/examples/) an explore!

===

I'm also developing more extra functions, called ["helpers"](https://github.com/flyingunicorn222/1broker-client/tree/v1/src/helpers) which will
hopefully simplify the implementation of mechanical tasks.

todo
====

- [x] Simple implementation
- [x] Examples
- [x] Tests
- [x] More Tests
- [ ] Extra methods ( long, short, close, reverse, [...] )
- [ ] Documentation
- [ ] Parameters validation
- [ ] Please [create an issue](https://github.com/flyingunicorn222/1broker-client/issues/new) if you need something else

contributing
====

**coding**

The source code is also pretty simple and self explainatory so feel free
to edit and submit a pull request.

**reports and requests**

[Please open an issue!](https://github.com/flyingunicorn222/1broker-client/issues/new), it will be highly appreciated.

**donate**

You can [donate to support this library and more freebies!](https://blockchain.info/address/1AsB6GtqUjHrLRXBzA19RMYyD7G9aVARbx)
a few happy users already donated and shown their love, the helped is much appreciated and needed as a lot of work is being invested on this library!

**BTC:** [*1AsB6GtqUjHrLRXBzA19RMYyD7G9aVARbx*](https://blockchain.info/address/1AsB6GtqUjHrLRXBzA19RMYyD7G9aVARbx)

![Thanks!](/docs/1AsB6GtqUjHrLRXBzA19RMYyD7G9aVARbx.png)

get in touch
====

Feel free to send me a message on reddit, I'm [flyingunicorn222](https://www.reddit.com/user/flyingunicorn222)

Thank You!

disclaimer
====
 - Altough this isn't an official [1Broker](https://1broker.com/?r=11468) client, they provided great support and cleared all questions, very kind guys!

 - The goal of this library is not only implement all current API methods but also add extra features, most of the extras are on the /helpers folder

 - By default when creating an order this library will use my referral_id,
that means I'll receive a small amount of BTC from [1Broker](https://1broker.com/?r=11468)
when you create an order! Please keep it this way so i can keep working on improving and impressing with this library!

 - [1broker](https://1broker.com/?r=11468) links on this documentation
constains my referral link, in case you still don't have an account please use those links to create it.
