# Near protocol's StackWar guide for DigitalOcean

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
##### Create new NEAR account
At Wallet page click "+Create New Account" button
![image](https://user-images.githubusercontent.com/17448647/180642421-eb6f4e08-86bf-4f3c-b8f5-b26c00a6384c.png)



##### Authorize Wallet Locally
A full access key needs to be installed locally to be able to sign transactions via NEAR-CLI.


* You need to run this command:

```
near login
```
![image](https://user-images.githubusercontent.com/17448647/180642711-b96950e6-ba24-4a6d-b447-ff358386e464.png)

> Note: This command launches a web browser allowing for the authorization of a full access key to be copied locally.

1 – Copy the link in your browser
![image](https://user-images.githubusercontent.com/17448647/180642759-cab79897-b06f-4073-b140-eb13a134eccf.png)
Chose account, Click "Next"
![image](https://user-images.githubusercontent.com/17448647/180642824-7d647678-de7b-4a58-87eb-352e290473a1.png)
Click "Connect" button

2 – Grant Access to Near CLI

![image](https://user-images.githubusercontent.com/17448647/180642853-e6e6c7bf-e552-4e5b-8601-dea4eccb4145.png)
Type your account and click Next

3 – After Grant, you will see a page like this, go back to console

![img](./images/4.png)

4 – Enter your wallet and press Enter

![image](https://user-images.githubusercontent.com/17448647/180642960-ae226417-1bfc-415f-a1c0-c0dcc64e58b9.png)


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
![image](https://user-images.githubusercontent.com/17448647/180656946-cf158d98-e472-4ffc-b8e0-b8a550ea878c.png)


* Copy the file generated to shardnet folder:
Make sure to replace <pool_id> by your accountId
```
cp ~/.near-credentials/shardnet/YOUR_WALLET.json ~/.near/validator_key.json
```
![image](https://user-images.githubusercontent.com/17448647/180657020-14129a8c-0123-432f-a638-51518e09530b.png)

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
![image](https://user-images.githubusercontent.com/17448647/180657281-8acc750c-4e07-48fa-acbf-8cc325c7a851.png)
![image](https://user-images.githubusercontent.com/17448647/180658090-57c4f648-6353-4f50-a341-eeff67ab11cc.png)


#####  Start the validator node

```
target/release/neard run
```
![image](https://user-images.githubusercontent.com/17448647/180658458-d61d64e6-f3eb-443c-9ef2-bcc41de4d020.png)

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
![image](https://user-images.githubusercontent.com/17448647/180658620-ea56255e-147c-4998-9eaf-19827b219542.png)

Command:

```
sudo systemctl enable neard
```
Command:

```
sudo systemctl start neard
```
![image](https://user-images.githubusercontent.com/17448647/180658652-ca3ff96a-2aa0-4cff-aa68-b6b26438bbe4.png)

If you need to make a change to service because of an error in the file. It has to be reloaded:

```
sudo systemctl reload neard
```
###### Watch logs
Command:

```
journalctl -n 100 -f -u neard
```
![image](https://user-images.githubusercontent.com/17448647/180658670-adfb0015-0eec-4f5a-b98d-9875b607c198.png)

Make log output in pretty print

Command:

```
sudo apt install ccze
```
![image](https://user-images.githubusercontent.com/17448647/180658701-cbfa9497-3ad8-4728-989f-ea541431e63d.png)

View Logs with color

Command:

```
journalctl -n 100 -f -u neard | ccze -A
```
![image](https://user-images.githubusercontent.com/17448647/180658735-092a52fc-3f09-4e66-933a-ac7b803da1a6.png)

## 3. Mounting a staking pool

NEAR uses a staking pool factory with a whitelisted staking contract to ensure delegators’ funds are safe. In order to run a validator on NEAR, a staking pool must be deployed to a NEAR account and integrated into a NEAR validator node. Delegators must use a UI or the command line to stake to the pool. A staking pool is a smart contract that is deployed to a NEAR account.

#### Deploy a Staking Pool Contract
##### Deploy a Staking Pool
Calls the staking pool factory, creates a new staking pool with the specified name, and deploys it to the indicated accountId.

```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "<pool id>", "owner_id": "<accountId>", "stake_public_key": "<public key>", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="<accountId>" --amount=30 --gas=300000000000000
```

From the example above, you need to replace:

* **Pool ID**: Staking pool name, the factory automatically adds its name to this parameter, creating {pool_id}.{staking_pool_factory}
Examples:   

- If pool id is stakewars will create : `stakewars.factory.shardnet.near`

* **Owner ID**: The SHARDNET account (i.e. stakewares.shardnet.near) that will manage the staking pool.
* **Public Key**: The public key in your **validator_key.json** file.
* **5**: The fee the pool will charge (e.g. in this case 5 over 100 is 5% of fees).
* **Account Id**: The SHARDNET account deploying and signing the mount tx.  Usually the same as the Owner ID.
In my case:
```
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "tonitest", "owner_id": "tonitest.shardnet.near", "stake_public_key": "ed25519:7QhoyFAMxcVBXncs7x7gC5RqTfGumoN1hb6QNaYg6WVb", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"DD428g9eqLL8fWUxv8QSpVFzyHi1Qd16P8ephYCTmMSZ"}' --accountId="tonitest.shardnet.near" --amount=30 --gas=300000000000000
```
![image](https://user-images.githubusercontent.com/17448647/180659226-39fe21d3-66fd-47c9-b385-a29b94af6d52.png)


> Be sure to have at least 30 NEAR available, it is the minimum required for storage.
Example : near call stake_wars_validator.factory.shardnet.near --amount 30 --accountId stakewars.shardnet.near --gas=300000000000000


To change the pool parameters, such as changing the amount of commission charged to 1% in the example below, use this command:
```
near call <pool_name> update_reward_fee_fraction '{"reward_fee_fraction": {"numerator": 1, "denominator": 100}}' --accountId <account_id> --gas=300000000000000
```


You will see something like this:

![img](./images/pool.png)

If there is a “True” at the End. Your pool is created.

**You have now configure your Staking pool.**

Check your pool is now visible on https://explorer.shardnet.near.org/nodes/validators
![image](https://user-images.githubusercontent.com/17448647/180659306-e6550da2-f2be-47bd-be17-c4ed400db665.png)


#### Transactions Guide
##### Deposit and Stake NEAR

Command:
```
near call <staking_pool_id> deposit_and_stake --amount <amount> --accountId <accountId> --gas=300000000000000
```
![image](https://user-images.githubusercontent.com/17448647/180659387-ecefcc7e-937a-4519-b80a-46378a62955d.png)

##### Unstake NEAR
Amount in yoctoNEAR.

Run the following command to unstake:
```
near call <staking_pool_id> unstake '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
```
To unstake all you can run this one:
```
near call <staking_pool_id> unstake_all --accountId <accountId> --gas=300000000000000
```
##### Withdraw

Unstaking takes 2-3 epochs to complete, after that period you can withdraw in YoctoNEAR from pool.

Command:
```
near call <staking_pool_id> withdraw '{"amount": "<amount yoctoNEAR>"}' --accountId <accountId> --gas=300000000000000
```
Command to withdraw all:
```
near call <staking_pool_id> withdraw_all --accountId <accountId> --gas=300000000000000
```

##### Ping
A ping issues a new proposal and updates the staking balances for your delegators. A ping should be issued each epoch to keep reported rewards current.

Command:
```
near call <staking_pool_id> ping '{}' --accountId <accountId> --gas=300000000000000
```
![image](https://user-images.githubusercontent.com/17448647/180659471-03f0e9d3-f0cb-4f97-827b-b818757eb99f.png)

Balances
Total Balance
Command:
```
near view <staking_pool_id> get_account_total_balance '{"account_id": "<accountId>"}'
```
##### Staked Balance
Command:
```
near view <staking_pool_id> get_account_staked_balance '{"account_id": "<accountId>"}'
```
##### Unstaked Balance
Command:
```
near view <staking_pool_id> get_account_unstaked_balance '{"account_id": "<accountId>"}'
```
##### Available for Withdrawal
You can only withdraw funds from a contract if they are unlocked.

Command:
```
near view <staking_pool_id> is_account_unstaked_balance_available '{"account_id": "<accountId>"}'
```
##### Pause / Resume Staking
###### Pause
Command:
```
near call <staking_pool_id> pause_staking '{}' --accountId <accountId>
```
###### Resume
Command:
```
near call <staking_pool_id> resume_staking '{}' --accountId <accountId>
```
### Monitor and make alerts 

An email notification can make it more comfortable to maintain a validator up and running. Achieve to be a validator confirming transactions on testnet and get >95% of uptime.

#### Log Files
The log file is stored either in the ~/.nearup/logs directory or in systemd depending on your setup.


Systemd Command:
```
journalctl -n 100 -f -u neard | ccze -A
```
![image](https://user-images.githubusercontent.com/17448647/180659556-15170a63-c99b-486a-969a-0830ec7a958d.png)

**Log file sample:**

Validator | 1 validator

```
INFO stats: #85079829 H1GUabkB7TW2K2yhZqZ7G47gnpS7ESqicDMNyb9EE6tf Validator 73 validators 30 peers ⬇ 506.1kiB/s ⬆ 428.3kiB/s 1.20 bps 62.08 Tgas/s CPU: 23%, Mem: 7.4 GiB
```

* **Validator**: A “Validator” will indicate you are an active validator
* **73 validators**: Total 73 validators on the network
* **30 peers**: You current have 30 peers. You need at least 3 peers to reach consensus and start validating
* **#46199418**: block – Look to ensure blocks are moving

#### RPC
Any node within the network offers RPC services on port 3030 as long as the port is open in the nodes firewall. The NEAR-CLI uses RPC calls behind the scenes. Common uses for RPC are to check on validator stats, node version and to see delegator stake, although it can be used to interact with the blockchain, accounts and contracts overall.

Find many commands and how to use them in more detail here:

https://docs.near.org/docs/api/rpc



Command:
```
sudo apt install curl jq
```
![image](https://user-images.githubusercontent.com/17448647/180659605-213411f3-8dc8-4a05-b8a7-59cd719f8612.png)

###### Common Commands:
####### Check your node version:
Command:
```
curl -s http://127.0.0.1:3030/status | jq .version
```
![image](https://user-images.githubusercontent.com/17448647/180659623-7d724342-8cbd-4a86-a137-a95170bebefa.png)

####### Check Delegators and Stake
Command:
```
near view <your pool>.factory.shardnet.near get_accounts '{"from_index": 0, "limit": 10}' --accountId <accountId>.shardnet.near
```
![image](https://user-images.githubusercontent.com/17448647/180659648-ea55ac27-a800-4f28-aed7-c5bf008dae12.png)

####### Check Reason Validator Kicked
Command:
```
curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.prev_epoch_kickout[] | select(.account_id | contains ("<POOL_ID>"))' | jq .reason
```
####### Check Blocks Produced / Expected
Command:
```
curl -s -d '{"jsonrpc": "2.0", "method": "validators", "id": "dontcare", "params": [null]}' -H 'Content-Type: application/json' 127.0.0.1:3030 | jq -c '.result.current_validators[] | select(.account_id | contains ("POOL_ID"))'
```
