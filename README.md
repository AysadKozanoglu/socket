# PHP Async Socket

## [Howto Installation and Quickstart  Documentation](https://github.com/AysadKozanoglu/socket/wiki)

https://github.com/AysadKozanoglu/socket/wiki


Thanks to : Dazzle

## Description

Dazzle Socket is a component that implements asynchronous tcp, udp and unix socket handling for PHP. The library also provides interface for implementing self inter-process communication via external services.

## Feature Highlights

Dazzle Socket features:

* Asynchronous handling of incoming and outcoming messages,
* Support for TCP, UDP and Unix sockets,
* ...and more.

## Provided Example(s)

### Quickstart

Server file which accepts the range in format of $min-$max and returns randomized number.

```php
$loop = new Loop(new SelectLoop);
$server = new SocketListener('tcp://127.0.0.1:2080', $loop);

$server->on('connect', function($server, SocketInterface $client) {
    $client->write("Hello!\n");
    $client->write("Welcome to Dazzle server!\n");
    $client->write("Tell me a range and I will randomize a number for you!\n\n");

    $client->on('data', function(SocketInterface $client, $data) use(&$buffer) {
        $client->write("Your number is: " . rand(...explode('-', $data)));
    });
});

$loop->onStart(function() use($server) {
    $server->start();
});
$loop->start();
```

Client file which sends the $min-$max format to the above server and gets the response.

```php
$loop = new Loop(new SelectLoop);
$socket = new Socket('tcp://127.0.0.1:2080', $loop);

$socket->on('data', function($socket, $data) {
    printf("%s", $data);
});
$socket->write('1-100');

$loop->start();
```

### Additional

Additional examples can be found in [example](https://github.com/AysadKozanoglu/socket/tree/master/example) directory. Below is the list of provided examples as a reference and preferred consumption order:

- [Quickstart](https://github.com/AysadKozanoglu/socket/blob/master/example/events_quickstart.php)
- [Using socket client](https://github.com/AysadKozanoglu/socket/blob/master/example/socket_only_client.php)
- [Using socket server](https://github.com/AysadKozanoglu/socket/blob/master/example/socket_only_server.php)
- [Creating TCP IPv4 client-server connection](https://github.com/AysadKozanoglu/socket/blob/master/example/socket_conn_tcp.php)
- [Creating TCP IPv6 client-server connection](https://github.com/AysadKozanoglu/socket/blob/master/example/socket_conn_tcp_ipv6.php)
- [Creating UNIX socket client-server connection](https://github.com/AysadKozanoglu/socket/blob/master/example/socket_conn_unix.php)
- [Getting connection info](https://github.com/AysadKozanoglu/socket/blob/master/example/socket_info.php)
- [Using secure SSL socket client](https://github.com/AysadKozanoglu/socket/blob/master/example/socket_ssl_only_client.php)
- [Using secure SSL socket server](https://github.com/AysadKozanoglu/socket/blob/master/example/socket_ssl_only_server.php)
- [Creating secure SSL client-server connection](https://github.com/AysadKozanoglu/socket/blob/master/example/socket_ssl.php)

If any of the above examples has left you confused, please take a look in the [tests](https://github.com/AysadKozanoglu/socket/tree/master/test) directory as well.


## Requirements

Dazzle Socket requires:

* PHP-5.6 or PHP-7.0+,
* UNIX or Linux


## License

Dazzle Socket is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).

