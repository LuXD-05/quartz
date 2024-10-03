### Client/Server paradigm

Data exchange between network apps takes place according to the ***Client/Server paradigm***, that says that a <u>client requires to communicate with a server</u>, which can respond or not.

###### API

Programming languages use **APIs** that provides tools for client/server tasks, such as C#’s "*System.Net.Sockets*" package.

##### Communication protocols

Communication between client & server is always ruled by a **protocol** that may involve:

- **Pull protocol** : (Ex: **HTTP**, used to ask & get web pages from servers) Client requests to **receive** data from the server.
- **Push protocol** : (Ex: **SMTP**, used to ask & send emails) Client requests to **send** data to the server.

Any activity in internet involving multiple remote hosts is ruled by the <u>TCP/IP protocol</u>.

### Communication models

##### Client/Server model

- App divided in <u>client program</u> and <u>server program</u>,
- **Client protocol** associated with **client program** in a **client host**,
- **Server protocol** associated with **server program** in a **server host** (generally ISP),
- ISP’s servers make up the infrastructure of internet services and run programs.

##### P2P model

- App = <u>single program</u>,
- **App** associated with **both client** and **server protocols**,
- <u>Client protocol</u> of a host requires communication to <u>server protocol</u> of another host,
- **Hosts** run P2P apps (like BitTorrent).

##### Hybrid model

- **Infrastructure** server program running on **ISP servers**,
- **P2P program** running **on** user **hosts**,
- **Phases**: 1) user contact server, 2) server bring the contact to another user, 3) contact set, involves now only clients.

### Services

###### Web Services

Apps that user accesses via **web apps** and through a **browser** (socials, Dropbox web, webmail, YouTube…).

###### Internet Services

Apps (client/server or P2P) that the user can access through a **specific program** (<u>not browser</u>) (WhatsApp desktop…).

