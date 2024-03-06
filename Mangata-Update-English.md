<h1 align="center"> Mangata AVS

# 01.03.2024 Update
# [CLICK HERE](#errors) for the meaning/solutions of the errors you encounter after updating.

# Update Steps

> Let's start the update process. 

> Before you start, the total amount of rETH and sETH you stake must be higher OR equal to 1ETH.

> [CLICK HERE](https://goerli.eigenlayer.xyz/) It should be higher or equal to 1ETH as shown in the picture below.
![picture](https://github.com/CoinHuntersTR/Mangata-AVS/assets/63106683/62f8e068-a665-489c-9c4f-22ed776604c7)


```
cd avs-operator-setup
```

```
docker compose down
```

> You need to back up your .env file. if you want, you can do nano .env and copy everything on the screen directly.

```
git reset --hard
```
```
git pull
```

```
docker compose pull
```
```
docker compose down
```

> We have updated our node files with the codes we previously wrote. 
> So we need to edit the updated env file.

```
nano .env
```

![picture](https://github.com/CoinHuntersTR/Mangata-AVS/assets/63106683/08656c4e-c446-4d38-a92a-f892e223549f)

> Edit the double fancy brackets in the picture based on the .env file we backed up. 
>**Do not touch anything else.** 

>***DELETE THE FANCY BRACKETS TOO!!!***

> If your env file is not like the picture, write the following codes.

```
rm -rf .env
```

```
nano .env
```

> Copy the code below and open it in a notepad **delete the fancy brackets** and write the required values.

> Then paste it into the .env file we just opened as a blank page and paste it with right click.

```
MAIN_SERVICE_IMAGE=mangatasolutions/avs-finalizer:80ac399c2c2f103dd8de1be62c114d5090cd11cd
MAIN_SERVICE_NAME=avs-finalizer-node

#COLORBT_SHOW_HIDDEN=1
#RUST_BACKTRACE=full

# Goerli contracts deployment
AVS_REGISTRY_COORDINATOR_ADDR=0x5620cDb94BaAaD10c20483bd8705DA711b2Bc0a3

# Finalizer Service Manager RPC
AVS_RPC_URL=https://avs-aggregator-testnet.mangata.online/
# register with AVS when the node starts
OPT_IN_AT_STARTUP=true

RUST_LOG=avs=info

###############################################################################
####### TODO: Operators please update below values for your node ##############
###############################################################################

# TODO: Operators need to update this to provide connection to ETH & network nodes
CHAIN_ID=5
ETH_RPC_URL={{RPC url https://goerli.infura.io/v3/ bla bla bla}}
ETH_WS_URL= {{Websocket url wss://goerli.infura.io/ws/v3/ bla bla bla}}
SUBSTRATE_RPC_URL=wss://collator-01-ws-rollup-testnet.mangata.online:443

# TODO: Operators need to update this to their own keys, either use files or encoded JSON
# this is where your keys are stored on local storage
ECDSA_KEY_FILE_HOST=/root/.eigenlayer/operator_keys/{{eigenlayer_wallet_name}}.ecdsa.key.json
BLS_KEY_FILE_HOST=/root/.eigenlayer/operator_keys/{{eigenlayer_wallet_name}}.bls.key.json

# this is where the node binary finds the keys in the docker container
ECDSA_KEY_FILE=/app/operator_keys/ecdsa_key.json
BLS_KEY_FILE=/app/operator_keys/bls_key.json

# it is possible to pass the encoded json key directly with these env flags
# comment above both ECDSA_KEY_FILE & BLS_KEY_FILE if used
#ECDSA_KEY_JSON=
#BLS_KEY_JSON=

# TODO: Operators need to add password to decrypt the above keys
ECDSA_KEY_PASSWORD={{YOUR_PASSWORD}}
BLS_KEY_PASSWORD={{YOUR_PASSWORD}}
```


> When you are done, your file should look like this picture.

![resim](https://github.com/CoinHuntersTR/Mangata-AVS/assets/63106683/918c7b2b-033c-4a5a-9620-6af2ebf03a68)

> When you're done with env

```
docker compose up -d
```

```
docker logs -f avs-finalizer-node
```

> Then it should look like the picture. 

![resim](https://github.com/CoinHuntersTR/Mangata-AVS/assets/63106683/b2ace762-4a95-4cef-a95d-795ed015c5db)

> But it may take a while for these logs to start flowing, right now the network is very slow.
> If it says Sucesfully registered as in the picture, leave it alone and don't worry too much. 
> If you do not see ✅ after 30 minutes, there may be a problem.
> Come to the Discord and let's solve the problem and we will also add it to the guide, it will be good for other node operators.

> Update Guide by @dwtexe 
> I wish you all the best.

## Announcement
## At the moment your node will not work properly. Mangata's RPC server (https://avs-aggregator-testnet.mangata.online/) is not working properly. 
## Therefore, it is natural to see RPC Errors in the [CLICK](#Errors) section below.
## There is nothing you can do, we are waiting for an announcement from the team.
## ![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/0342eaa6-1f64-475e-9a68-94620c3d8078)
## If your node is like the picture above, it means that there is no problem, rpc errors will appear on the screen soon, do not worry, you have completed the installation without any problems.
## Announcement over.


# Errors

> 24 hours later, I'm back here.

> Yes, now let's explain the mistakes that everyone asks and does not get tired of asking, and if there are solutions, let's solve them.


### 1 - RPC Errors

> The following errors are called RPC errors. They are not related to you and you will not find a solution even if you try to find one, so stop asking.

> This is a problem that Mangata has to solve, we will wait to hear from them, there is **nothing** can we do.

![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/8fdbac8d-4b6c-43a6-aceb-07e47b30e23f)
![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/6da44650-3590-49ec-8d02-fa64c8c67b6f)
![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/d81e1339-9f99-4356-a9c3-5bd53c46ae58)
![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/c45ee3e7-1c75-4338-9418-a40614685526) 


### 2 - .env Errors

> Let's talk about the second most common errors.

> There is no other possibility that these errors are caused by you!

> This error means that there is an error in your .env file.

> Compare the empty and the final version of the .env file I posted above, and check and recheck until you are sure that you have only changed the parts I said to change properly.

> Some friends forget their passwords and even if every part is correct, they get errors and tear themselves apart. Please be sure of your password.

![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/fc7d7b20-4894-4208-a403-d0673a7063a7)
![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/984c1f42-1cc8-41dd-b018-383d11d22922)

### 3 - No log progress

> Wait a little, the logs will appear, but they may not appear, at the moment there is an rpc problem that the mangata team needs to fix.

> I don't think there is anyone who runs Node smoothly and error-free.

> Occasionally logs appear, then we get an error, then it seems to be fixed again, etc. So don't worry too much and wait for news from the Mangata team.

![resim](https://github.com/Dwtexe/Mangata-AVS/assets/63106683/0342eaa6-1f64-475e-9a68-94620c3d8078)


> Finally, please contact me if there are any bugs that you have solved or even if you cannot solve them, you understand why they are caused.
> Telegram/Discord : @dwtexe
