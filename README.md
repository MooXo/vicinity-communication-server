# What is VICINITY Communication Server?
The VICINITY Communication Server is VICINITY Cloud component which facilitates communication between peers ([VICINITY Agents](https://github.com/vicinityh2020/vicinity-agent)) in peer-to-peer (P2P) network VICINITY Platform thorugh Open VICINITY Gateway API. The VICINITY Communication Server is based on implementation of (Extensible Messaging and Presence Protocol) XMPP OpenFire to provide high-available and secure communication environment in VICINITY platform. VICINITY Communication Server is tightly connected to [VICINITY Neighbourhood Manager](https://github.com/vicinityh2020/vicinity-neighbourhood-manager), which defines the communication rules in peer-to-peer network and VICINITY Communciation Server enforces these rules in peer-to-peer network through XMPP shared rosters mechanism.


# Installation

The Communication Server needs to have three packages installed in order to work properly:

* [MySQL database server](https://dev.mysql.com/doc/relnotes/mysql/5.5/en/news-5-5-59.html),
* [Openfire XMPP server 4.1.3](https://www.igniterealtime.org/projects/openfire/index.jsp),
* [VICINITY Neighbourhood Manager](https://github.com/vicinityh2020/vicinity-neighbourhood-manager) installed and configured.

Having said that, necessary steps are following:

1. Install MySQL server and [create a separate user](http://download.igniterealtime.org/openfire/docs/latest/documentation/database.html) for the Openfire XMPP server.
2. Install [Openfire XMPP server](http://download.igniterealtime.org/openfire/docs/latest/documentation/install-guide.html), and during installation configure it to use MySQL server on local host, with credentials from step 1.
3. Install [VICINITY Neighbourhood Manager](https://github.com/vicinityh2020/vicinity-neighbourhood-manager).

Observe proper steps in documentation for each software.

# Configuration

There are some configuration parameters that has to be set in Openfire XMPP server configuration. First, the REST API plugin must be installed, security certificates needs to be correctly configured and some minor tweaks need to be done to group properties.

1.	Install the [REST API Openfire plugin](https://www.igniterealtime.org/projects/openfire/plugins/restapi/readme.html) according to the documentation for your version of Openfire.
2.	Get certificates signed by proper certification authority. Then import them into your server's [Java keystore](https://docs.oracle.com/javase/tutorial/security/toolfilex/rstep1.html). Openfire is written in Java and instead of importing particular certificates, it imports whole Java keystore.
3.	In the web based administration interface of Openfire, go to System Properties and add these three records to confifgure the Openfire NOT to cache information about groups, making any direct changes to the group records done by the Collaboration Web effective immediately:


```

	cache.group.maxLifetime         set to value '1' 
	cache.groupMeta.maxLifetime     set to value '1' 
	cache.userGroup.maxLifetime     set to value '1' 

```

