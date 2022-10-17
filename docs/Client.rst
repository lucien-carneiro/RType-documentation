**************
Part 2: Client
**************

Description
===========
The client is the display terminal of the game.
To rendering audio, input and network, we use the SFML and the BOOST libraries.

Initialisation
==============

Client interface
****************
Here is Client class constructor:

.. code:: python

    self.team = team_name
    self.hostname = hostname
    self.port = port
    self.client_num = 0
    self.data = Data(0, 0)
    self.socket = None
    self.selectors = selectors.DefaultSelector()
    self.just_log = 0
    self.logged = 0
    self.ia = IA(self.team)

Server Connection
*****************
Initialise a socket which connects to the server.
We initialize the selectors to and be sure to receive the Welcome message.

.. code:: python

    def connect_to_server(self):
        self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.socket.setblocking(False)
        self.socket.connect_ex((self.hostname, safe_cast(self.port, int)))
        events = selectors.EVENT_READ | selectors.EVENT_WRITE
