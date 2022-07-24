# War

```
node -v
```
> v18.x.x

```
npm -v
```
> 8.x.x

#### Regist a VPS:
Login https://cloud.digitalocean.com
Click "Droplets" manu
![image](https://user-images.githubusercontent.com/17448647/180631318-c5663105-8d4c-4dfe-983f-ed2a844f2232.png)
Click "Create Droplet" button
![image](https://user-images.githubusercontent.com/17448647/180631310-e0e77d18-1e86-4353-88a3-e1a56f6b7d58.png)
Chose your plan. Mine is Ubuntu, Basic, 4 CPUs, 8 GB, 160 GB SSD, just for demo how to install.
![image](https://user-images.githubusercontent.com/17448647/180631447-35d18ca3-a405-487f-b69b-1a03cb704d2f.png)
Chose Region whatever you want
![image](https://user-images.githubusercontent.com/17448647/180631516-5b1022f1-d988-4b76-9068-87ef3dee7f69.png)
Create your password
![image](https://user-images.githubusercontent.com/17448647/180631571-a9563127-a595-417c-a8d3-3d0cc1a76203.png)
Press "Create Droplet" button
![image](https://user-images.githubusercontent.com/17448647/180631600-045dc558-9473-4964-ae13-f1c640bf9412.png)
Wait 5 minutes to see your new Droplet
![image](https://user-images.githubusercontent.com/17448647/180631696-9db1a65b-4edb-4365-8fa5-4660306ac7ad.png)


#### Connect to VPS using Putty:
Click on "..." button then click "Access console"
![image](https://user-images.githubusercontent.com/17448647/180631750-5323de2f-83d6-4972-a338-b19df5a864b3.png)
Click on "Lauch Droplet Console" button (or you can use Putty)
![image](https://user-images.githubusercontent.com/17448647/180631811-77ecd08b-30c2-4240-a851-d1879369b550.png)
A pop-up window is shown, that means you are connected
![image](https://user-images.githubusercontent.com/17448647/180631845-90b68f62-b764-49b0-be50-ebbed0f788e3.png)

#### Setup NEAR-CLI

NEAR-CLI is a command-line interface that communicates with the NEAR blockchain via remote procedure calls (RPC):

* Setup and Installation NEAR CLI
* View Validator Stats

> Note: For security reasons, it is recommended that NEAR-CLI be installed on a different computer than your validator node and that no full access keys be kept on your validator node.

First, let's make sure the linux machine is up-to-date.
```
sudo apt update && sudo apt upgrade -y
```
Result:
![image](https://user-images.githubusercontent.com/17448647/180632506-d56c5551-bcdd-4b61-b478-3dbe6ed515c7.png)

##### Install developer tools, Node.js, and npm
First, we will start with installing `Node.js` and `npm`:
```
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -  
sudo apt install build-essential nodejs
PATH="$PATH"
```
Result:
![image](https://user-images.githubusercontent.com/17448647/180632552-7f922160-969f-44f1-b1c5-5c19dc87ecec.png)


Check `Node.js` and `npm` version:
```
node -v
```
> v18.x.x
 ![image](https://user-images.githubusercontent.com/17448647/180632567-63a203c8-9438-4a9b-af39-179e5d0482df.png)


```
npm -v
```
> 8.x.x
![image](https://user-images.githubusercontent.com/17448647/180632585-bf7daa01-0fb0-4771-8e8c-7fff9ecccd82.png)


##### Install NEAR-CLI
Here's the Github Repository for NEAR CLI.: https://github.com/near/near-cli. To install NEAR-CLI, unless you are logged in as root, which is not recommended you will need to use `sudo` to install NEAR-CLI so that the near binary is saved to /usr/local/bin

```
sudo npm install -g near-cli
```
![image](https://user-images.githubusercontent.com/17448647/180632651-be15b4c5-f77d-4318-bd69-5b63abeda857.png)


### Validator Stats

Now that NEAR-CLI is installed, let's test out the CLI and use the following commands to interact with the blockchain as well as to view validator stats. There are three reports used to monitor validator status:


###### Environment
The environment will need to be set each time a new shell is launched to select the correct network.

Networks:
- GuildNet
- TestNet
- MainNet
- **Shardnet** (this is the network we will use for Stake Wars)

Command:
```
export NEAR_ENV=shardnet
```

You can also run this command to set the Near testnet Environment persistent:
```
echo 'export NEAR_ENV=shardnet' >> ~/.bashrc
```
![image](https://user-images.githubusercontent.com/17448647/180632678-a6339691-febb-4fe3-a7c6-7bec61d6d644.png)

#### NEAR CLI Commands Guide:

###### Proposals
A proposal by a validator indicates they would like to enter the validator set, in order for a proposal to be accepted it must meet the minimum seat price.

Command:
```
near proposals
```
![image](https://user-images.githubusercontent.com/17448647/180632709-02dd31e3-f344-453b-b33d-a53be8b0cbca.png)

###### Validators Current
This shows a list of active validators in the current epoch, the number of blocks produced, number of blocks expected, and online rate. Used to monitor if a validator is having issues.

Command:
```
near validators current
```
![image](https://user-images.githubusercontent.com/17448647/180632740-a56191d1-623b-4112-ab92-07d389f3b94e.png)


###### Validators Next
This shows validators whose proposal was accepted one epoch ago, and that will enter the validator set in the next epoch.

Command:
```
near validators next
```
![image](https://user-images.githubusercontent.com/17448647/180632814-77307417-0416-44b3-bbb7-ac61346d5f14.png)

### Setup your node
#### Server Requirements
Please see the hardware requirement below:

| Hardware       | Chunk-Only Producer  Specifications                                   |
| -------------- | ---------------------------------------------------------------       |
| CPU            | 4-Core CPU with AVX support                                           |
| RAM            | 8GB DDR4                                                              |
| Storage        | 500GB SSD                                                             |


#### Install required software & set the configuration

##### Prerequisites:
Before you start, you may want to confirm that your machine has the right CPU features. 

```
lscpu | grep -P '(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )' > /dev/null \
  && echo "Supported" \
  || echo "Not supported"
```
> Supported
![image](https://user-images.githubusercontent.com/17448647/180632881-cecff2de-5e17-4405-85aa-9f777928fabe.png)


##### Install developer tools:
```
sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python docker.io protobuf-compiler libssl-dev pkg-config clang llvm cargo
```

If you receive "E: Package 'python' has no installation candidate" error, you can use below command instead:
```
sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python2.7 docker.io protobuf-compiler libssl-dev pkg-config clang llvm cargo
```
![image](https://user-images.githubusercontent.com/17448647/180633164-72698073-1972-47d7-bef8-1a7bf0b1417d.png)


#####  Install Python pip:

```
sudo apt install python3-pip
```
![image](https://user-images.githubusercontent.com/17448647/180640090-f928a234-65d6-455f-b7ca-08b3858a8049.png)


##### Set the configuration:

```
USER_BASE_BIN=$(python3 -m site --user-base)/bin
export PATH="$USER_BASE_BIN:$PATH"
```
![image](https://user-images.githubusercontent.com/17448647/180640108-d6844f6b-4da0-42c8-89b9-7663a9c04d71.png)

##### Install Building env
```
sudo apt install clang build-essential make
```
![image](https://user-images.githubusercontent.com/17448647/180640123-09ae2bf9-cb91-4fee-99bc-7067e97a61f8.png)

##### Install Rust & Cargo
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

You will see the following:

![image](https://user-images.githubusercontent.com/17448647/180640180-f977c484-ffd1-49e5-865a-d432c3a3e468.png)

Press 1 and press enter.
![image](https://user-images.githubusercontent.com/17448647/180640192-e90a04c0-1cd0-43d8-a54c-a0ed12e74bb0.png)


##### Source the environment
```
source $HOME/.cargo/env
```
![image](https://user-images.githubusercontent.com/17448647/180640215-22ab8734-a04b-4fd8-af55-7477b6a6df6a.png)

#### Clone `nearcore` project from GitHub
First, clone the [`nearcore` repository](https://github.com/near/nearcore).

```
git clone https://github.com/near/nearcore
cd nearcore
git fetch
```
![image](https://user-images.githubusercontent.com/17448647/180640265-b403a7b0-5fde-4858-945d-7fa820cd7915.png)

Checkout to the commit needed. Please refer to the commit defined in [this file](https://github.com/near/stakewars-iii/blob/main/commit.md). 
```
git checkout <commit>
```
![image](https://user-images.githubusercontent.com/17448647/180640350-bff79b70-6312-4a02-935e-7f120063b10e.png)

#### Compile `nearcore` binary
In the `nearcore` folder run the following commands:

```
cargo build -p neard --release --features shardnet
```
![image](https://user-images.githubusercontent.com/17448647/180641092-5c980038-cc2e-4bfd-a43f-22a4559ba5a8.png)

The binary path is `target/release/neard`. If you are seeing issues, it is possible that cargo command is not found. Compiling `nearcore` binary may take a little while.

#### Initialize working directory

In order to work properly, the NEAR node requires a working directory and a couple of configuration files. Generate the initial required working directory by running:

```
./target/release/neard --home ~/.near init --chain-id shardnet --download-genesis
```
![image](https://user-images.githubusercontent.com/17448647/180641182-cbf1a7b7-2003-45be-814c-2f0a2359ab5a.png)


![img](./images/initialize.png)

This command will create the directory structure and will generate `config.json`, `node_key.json`, and `genesis.json` on the network you have passed. 

- `config.json` - Configuration parameters which are responsive for how the node will work. The config.json contains needed information for a node to run on the network, how to communicate with peers, and how to reach consensus. Although some options are configurable. In general validators have opted to use the default config.json provided.

- `genesis.json` - A file with all the data the network started with at genesis. This contains initial accounts, contracts, access keys, and other records which represents the initial state of the blockchain. The genesis.json file is a snapshot of the network state at a point in time. In contacts accounts, balances, active validators, and other information about the network. 

- `node_key.json` -  A file which contains a public and private key for the node. Also includes an optional `account_id` parameter which is required to run a validator node (not covered in this doc).

- `data/` -  A folder in which a NEAR node will write it's state.

#### Replace the `config.json`

From the generated `config.json`, there two parameters to modify:
- `boot_nodes`: If you had not specify the boot nodes to use during init in Step 3, the generated `config.json` shows an empty array, so we will need to replace it with a full one specifying the boot nodes.
- `tracked_shards`: In the generated `config.json`, this field is an empty. You will have to replace it to `"tracked_shards": [0]`

```
rm ~/.near/config.json
wget -O ~/.near/config.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/config.json
```
![image](https://user-images.githubusercontent.com/17448647/180641258-aa73f533-a362-4c08-9587-f7871206774a.png)

#### Get latest snapshot

**IMPORTANT: NOT REQUIRED TO GET SNAPSHOT AFTER HARDFORK ON SHARDNET DURING 2022-07-18**

Install AWS Cli
```
sudo apt-get install awscli -y
```
![image](https://user-images.githubusercontent.com/17448647/180641360-0e00514c-778c-4a7a-a054-ac3d45c59187.png)


Download snapshot (genesis.json)
```
// IMPORTANT: NOT REQUIRED TO GET SNAPSHOT AFTER HARDFORK ON SHARDNET DURING 2022-07-18
cd ~/.near
wget https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/genesis.json
```
![image](https://user-images.githubusercontent.com/17448647/180641388-85cbe832-42a0-41d7-83f6-9148aeb00aa6.png)


If the above fails, AWS CLI may be oudated in your distribution repository. Instead, try:
```
pip3 install awscli --upgrade
```

#### Run the node
To start your node simply run the following command:

```
cd ~/nearcore
./target/release/neard --home ~/.near run
```
![image](https://user-images.githubusercontent.com/17448647/180641449-91815b82-404f-4d66-adc7-6b98d0c4fe9f.png)

![img](./images/download.png)
The node is now running you can see log outputs in your console. Your node should be find peers, download headers to 100%, and then download blocks.
----

### Activating the node as validator
##### Authorize Wallet Locally
A full access key needs to be installed locally to be able to sign transactions via NEAR-CLI.


* You need to run this command:

```
near login
```

> Note: This command launches a web browser allowing for the authorization of a full access key to be copied locally.

1 – Copy the link in your browser


![img](./images/1.png)

2 – Grant Access to Near CLI

![img](./images/3.png)

3 – After Grant, you will see a page like this, go back to console

![img](./images/4.png)

4 – Enter your wallet and press Enter

![img](./images/5.png)


#####  Check the validator_key.json
* Run the following command:
```
cat ~/.near/validator_key.json
```


> Note: If a validator_key.json is not present, follow these steps to create one

Create a `validator_key.json` 

*   Generate the Key file:

```
near generate-key <pool_id>
```
<pool_id> ---> xx.factory.shardnet.near WHERE xx is you pool name

* Copy the file generated to shardnet folder:
Make sure to replace <pool_id> by your accountId
```
cp ~/.near-credentials/shardnet/YOUR_WALLET.json ~/.near/validator_key.json
```
* Edit “account_id” => xx.factory.shardnet.near, where xx is your PoolName
* Change `private_key` to `secret_key`

> Note: The account_id must match the staking pool contract name or you will not be able to sign blocks.\

File content must be in the following pattern:
```
{
  "account_id": "xx.factory.shardnet.near",
  "public_key": "ed25519:HeaBJ3xLgvZacQWmEctTeUqyfSU4SDEnEwckWxd92W2G",
  "secret_key": "ed25519:****"
}
```

#####  Start the validator node

```
target/release/neard run
```
* Setup Systemd
Command:

```
sudo vi /etc/systemd/system/neard.service
```
Paste:

```
[Unit]
Description=NEARd Daemon Service

[Service]
Type=simple
User=<USER>
#Group=near
WorkingDirectory=/home/<USER>/.near
ExecStart=/home/<USER>/nearcore/target/release/neard run
Restart=on-failure
RestartSec=30
KillSignal=SIGINT
TimeoutStopSec=45
KillMode=mixed

[Install]
WantedBy=multi-user.target
```

> Note: Change USER to your paths

Command:

```
sudo systemctl enable neard
```
Command:

```
sudo systemctl start neard
```
If you need to make a change to service because of an error in the file. It has to be reloaded:

```
sudo systemctl reload neard
```
###### Watch logs
Command:

```
journalctl -n 100 -f -u neard
```
Make log output in pretty print

Command:

```
sudo apt install ccze
```
View Logs with color

Command:

```
journalctl -n 100 -f -u neard | ccze -A
```
#### Becoming a Validator
In order to become a validator and enter the validator set, a minimum set of success criteria must be met.

* The node must be fully synced
* The `validator_key.json` must be in place
* The contract must be initialized with the public_key in `validator_key.json`
* The account_id must be set to the staking pool contract id
* There must be enough delegations to meet the minimum seat price. See the seat price [here](https://explorer.shardnet.near.org/nodes/validators).
* A proposal must be submitted by pinging the contract
* Once a proposal is accepted a validator must wait 2-3 epoch to enter the validator set
* Once in the validator set the validator must produce great than 90% of assigned blocks

Check running status of validator node. If “Validator” is showing up, your pool is selected in the current validators list.
---

