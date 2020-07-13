### It is recommended that you use the test server first

The official address [API2](https://www.gatecn.io/api2) [API4](https://www.gatecn.io/docs/futures/api/index.html)

All interface methods are initialized the same as those provided by Bitmex. See details [src/api](https://github.com/zhouaini528/gate-php/tree/master/src/Api)

Most of the interface is now complete, and the user can continue to extend it based on my design, working with me to improve it.

### Other exchanges API

[Exchanges](https://github.com/zhouaini528/exchanges-php) It includes all of the following exchanges and is highly recommended.

[Bitmex](https://github.com/zhouaini528/bitmex-php)

[Okex](https://github.com/zhouaini528/okex-php)

[Huobi](https://github.com/zhouaini528/huobi-php)

[Binance](https://github.com/zhouaini528/binance-php)

[Kucoin](https://github.com/zhouaini528/Kucoin-php)

[Mxc](https://github.com/zhouaini528/mxc-php)

[Coinbase](https://github.com/zhouaini528/coinbase-php)

[ZB](https://github.com/zhouaini528/zb-php)

[Bitfinex](https://github.com/zhouaini528/zb-php)

[Bittrex](https://github.com/zhouaini528/bittrex-php)

[Gate](https://github.com/zhouaini528/gate-php)

#### Installation
```
composer require linwj/gate
```

Support for more request Settings
```php
$gate=new Gate();

//You can set special needs
$gate->setOptions([
    //Set the request timeout to 60 seconds by default
    'timeout'=>10,
    
    //If you are developing locally and need an agent, you can set this
    'proxy'=>true,
    //More flexible Settings
    /* 'proxy'=>[
     'http'  => 'http://127.0.0.1:12333',
     'https' => 'http://127.0.0.1:12333',
     'no'    =>  ['.cn']
     ], */
    //Close the certificate
    //'verify'=>false,
]);
```

### Spot Public

Market related API [More](https://github.com/zhouaini528/gate-php/blob/master/tests/spot/public.php)

```php
$gate=new GateSpot();

try {
    $result=$gate->publics()->pairs();
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}


try {
    $result=$gate->publics()->marketinfo();
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
```

### Spot Private
```php
$gate=new GateSpot($key,$secret);

//bargaining transaction
try {
    $result=$gate->privates()->buy([
        'currencyPair'=>'btc_usdt',
        'rate'=>'3000',
        'amount'=>'0.01',
        //'text'=>'t-xxxxxxxxxx'
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

//track the order
try {
    $result=$gate->privates()->getOrder([
        'currencyPair'=>'btc_usdt',
        'orderNumber'=>'xxxxxxxxxx',
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

//cancellation of order
try {
    $result=$gate->privates()->cancelOrder([
        'currencyPair'=>'btc_usdt',
        'orderNumber'=>'xxxxxxxxxx',
    ]);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

//more
try {
    $result=$gate->privates()->balances();
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}

try {
    $result=$gate->privates()->depositAddress(['currency'=>'BTC']);
    print_r($result);
}catch (\Exception $e){
    print_r(json_decode($e->getMessage(),true));
}
```
