# Svarog

## Intro
Svarog is a development framework that enables developers to seamlessly run and query Substrate networks of their choice locally.



# How to


## Project structure
To initiate a Substrate network node of your choice, begin by creating a **/runners** directory to store the binaries of the desired networks you wish to instantiate.

## Important Note:

The binary's naming is crucial, as the name serves as the identifier to launch the network and fetch the network provider. There is an example of the Svarog runner in action available at [svarog-test](https://github.com/Ceres-Blockchain-Solutions/svarog-test). In this example, the pre-built Substrate Frame node template was used. **However, we recommend building the desired node on your own machine, as otherwise, there is a chance that the runner may not function properly.**


### Example

If a user intends to run a network utilizing the Substrate Frame node template, they should position the appropriately named **frame** binary (the Substrate frame node binary file) within the **/runners** directory. Take a look at the given example above.



## Running a network

Once you've imported your desired library, simply execute the command `npx svarog [binary]` in your terminal, where "binary" represents the name of your preferred node binary.

### Note
The terminal where the affirmation command is executed must remain open for the network to stay operational. Closing the terminal will result in the network shutting down.

By default, Svarog will instantiate a network consisting of 3 nodes. Svarog has the capacity to concurrently run up to 3 different Substrate-based networks, as two identical networks cannot run simultaneously.


### Port allocation

Svarog will, by default, utilize ports 10000 to 10800 (HTTP ports), 9944 to 9952 (WS/RPC ports), and 9954 to 9962 (RPC ports). Ensure that these ports are available on your local machine to successfully leverage Svarog.



## Connecting to network

To establish a connection to a Svarog-enabled network, utilize the supplied *getNetworkProvider()* function. This function retrieves the desired network connection URL based on the binary name and the preferred connection type.

### Example

Continuing from the earlier example, if a user has instantiated a Frame node network and intends to connect to it through a WebSocket connection, they would employ the following code snippet:

```node
import { getNetworkProvider } from "svarog/utils";
import { ApiPromise, WsProvider } from "@polkadot/api";

const main = async () => {
    const url = await getNetworkProvider("frame", "ws");

    const provider = new WsProvider(url);
    const api = await new ApiPromise({ provider }).isReady;
};

main()
    .catch((e) => {
        console.error(e);
        process.exit(1);
    })
    .finally(() => {
        process.exit(0);
    });
```


## Stopping a network

To stop a network, simply press Ctrl + C in the terminal where the initial network start command is running, or alternatively, close the terminal itself.

