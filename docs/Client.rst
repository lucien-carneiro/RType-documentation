**************
Part 2: Client
**************

Description
===========
The client is the display terminal of the game.
To rendering audio, input and network, we use the SFML and the BOOST libraries.

Client Connection
=================
Initialise a socket which connects to the server.
The client sends a packet to the server to identify itself.

.. code:: cpp

    void connect_to_server(void):
        udp::endpoint endpoint(boost::asio::ip::address::from_string(host), stoi(port));
        boost::asio::socket_base::reuse_address option(true);
        this->socket.open(udp::v4());
        this->socket.set_option(option);
        this->socket.bind(this->remote_endpoint);
        this->remote_endpoint = endpoint;
