Psiphon Circumvention System
================================================================================

Psiphon uses many code repositories for different parts of our system. This is a meta-repo with general information about the Psiphon Circumvention System.

**For downloads and more info about Psiphon and Psiphon Inc., please visit our web site at [psiphon.ca](https://www.psiphon.ca)**


Source Repositories
--------------------------------------------------------------------------------

These are the repos that will likely be of primary interest:

* https://github.com/Psiphon-Labs/psiphon-tunnel-core : Cross-platform "tunnel core" client engine and libraries
* https://github.com/Psiphon-Inc/psiphon-android : Android app
* https://github.com/Psiphon-Inc/psiphon-ios-vpn : iOS VPN app
* https://github.com/Psiphon-Inc/psiphon-windows : Windows application
* https://github.com/Psiphon-Inc/psiphon-automation : Tools for managing the Psiphon server network
* https://github.com/Psiphon-Inc/psiphon-website : Psiphon "download site"; e.g., at https://psiphon.ca/en/index.html and https://psiphon3.com

All of our public repositories can be found at https://github.com/Psiphon-Inc and
https://github.com/Psiphon-Labs.


System Overview
--------------------------------------------------------------------------------

The Psiphon Circumvention System is a relay-based Internet censorship
circumventer.

The system consists of a client application, which configures a user's computer
to direct Internet traffic; and a set of servers, which proxy client traffic to
the Internet. As long as a client can connect to a Psiphon server, it can
access Internet services that may be blocked to the user via direct connection.

Features:

- Automatic discovery. Psiphon clients ship with a set of known Psiphon
  servers to connect to. Over time, clients discover additional servers that are
  added to a backup server list. As older servers become blocked, each client will
  have a reserve list of new servers to draw from as it reconnects. To ensure that
  an adversary cannot enumerate and block a large number of servers, the Psiphon
  system takes special measures to control how many servers may be discovered by
  a single client.

- Cross-platform. Psiphon clients are available for Windows, Android, and iOS.

- Zero install. Psiphon is delivered to users as a minimal footprint, zero
  install application that can be downloaded from any webpage, file sharing site
  or shared by e-mail and passed around on a USB key. We keep the file size small
  and avoid the overhead of having to install an application.

- Custom branding.  Psiphon offers a flexible sponsorship system which
  includes sponsor-branded clients. Dynamic branding includes graphics and text on
  the client UI; and a region-specific dynamic homepage mechanism that allows a
  different home page to open depending on where in the world the client is run.

- Chain of trust. Each client instance may be digitally signed to certify its
  authenticity. Embedded server certificates certify that Psiphon servers the
  client connects to are the authentic servers for that client.

- Privacy. Psiphon is designed to respect user privacy. User statistics are
  logged in aggregate, but no individual personally identifying information, such
  as user IP addresses, are retained in Psiphon log files.

- Agile transport. Psiphon features a pluggable architecture with multiple
  transport mechanisms. In the case where one
  transport protocol is blocked by a censor, Psiphon automatically switches over
  to another mechanism.

Our [legacy design document](files/DESIGN.pdf) is outdated, but many of the
fundamentals still apply.


Security Properties
--------------------------------------------------------------------------------

Psiphon is a circumvention system. To accomplish its design goals, it uses computer
security technology including encryption and digital signatures. Using these algorithms
does not mean Psiphon offers additional security properties such as privacy or
authentication of destination sites for users' Internet traffic.

- Confidentiality. Traffic routed between a user's computer and a Psiphon proxy is encrypted
and authenticated. The purpose of this
encryption is to evade censorship based on deep-packet inspection of traffic, not to add
confidentiality to the user's Internet traffic. The user's traffic is plaintext to the Psiphon
proxy and to the Internet at large as it egresses from the Psiphon proxy. Put simply,
Psiphon does not add HTTPS or equivalent security where it is not already in place at the
application level.

- Anonymity. Psiphon is not an anonymity solution such as
[Tor](https://www.torproject.org).
If a user connects to a Psiphon proxy which is beyond the monitoring of the censor he or she
is circumventing, then the censor will only see that the user is sending encrypted traffic to
a Psiphon proxy. The censor will know the user is using Psiphon. Psiphon does not defend against
traffic analysis attacks the censor may deploy against traffic flowing to Psiphon proxies.
The Psiphon proxy will know where the user is coming from, what their unencrypted traffic is, and
what their destination is, and so the user is necessarily putting trust in the entity running the
Psiphon proxy.

- Integrity. Psiphon was not designed to add integrity to Internet traffic. However, in the case
where a censor is intercepting SSL/TLS traffic using compromised root CA keys, Psiphon adds
integrity; but only if the user has secured a trusted client out of band and is using a Psiphon
proxy beyond the control of the censor. Simply, the user's HTTPS traffic happens to bypass the
censors man-in-the-middle attack, and the Psiphon authentication system does not rely on the
commercial Certificate Authority for most use cases. See the design paper for details on
Psiphon PKI.

- Availability. Psiphon is designed to make available Internet content that's otherwise censored.
This is its primary design goal.


Licensing
--------------------------------------------------------------------------------

Please see the LICENSE files in the individual code repos. Most code is GPLv3; some
libraries have more permissive licenses.
