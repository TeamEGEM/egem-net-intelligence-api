EGEM Network Intelligence API
============

This is the backend service which runs along with EGEM and tracks the network status, fetches information through JSON-RPC and connects through WebSockets to [egem-netstats](https://github.com/TeamEGEM/egem-netstats) to feed information.


## Prerequisite
* geth
* node
* npm


## Installation
```bash
sudo npm install -g pm2
npm install
```
## Configuration

Configure the app modifying [processes.json](/egem-net-intelligence-api/blob/master/processes.json). Note that you have to modify the backup processes.json file located in `./bin/processes.json` (to allow you to set your env vars without being rewritten when updating).

```json
"env":
	{
		"NODE_ENV"        : "production", // tell the client we're in production environment
		"RPC_HOST"        : "localhost", // eth JSON-RPC host
		"RPC_PORT"        : "8545", // eth JSON-RPC port
		"LISTENING_PORT"  : "30303", // eth listening port (only used for display)
		"INSTANCE_NAME"   : "", // whatever you wish to name your node
		"CONTACT_DETAILS" : "", // add your contact details here if you wish (email/skype)
		"WS_SERVER"       : "http://network.egem.io/", // path to egem-netstats WebSockets api server
		"WS_SECRET"       : "PLEASE CONTACT EGEM STAFF - THIS WILL BE PUBLIC IN FUTURE", // WebSockets api server secret used for login
		"VERBOSITY"       : 2 // Set the verbosity (0 = silent, 1 = error, warn, 2 = error, warn, info, success, 3 = all logs)
	}
```

## Run

Run it using pm2:

```bash
cd ~/bin
pm2 start processes.json
```

## Updating

To update the API client use the following command:

```bash
~/bin/www/bin/update.sh
```

It will stop the current netstats client processes, automatically detect your ethereum implementation and version, update it to the latest develop build, update netstats client and reload the processes.

