# Proof of Authority

I started out by installing [Go Ethereum](https://geth.ethereum.org/downloads/) Tools by clicking on the 64-bit "Geth & Tools" archive. Once that downloaded, I extracted the zipped folder into a network folder that I created. The folder should contain the files shown in the screenshot below.

![Picture 1](https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/1.JPG)

### Create the Genesis

Navigate to the folder that you created above in your terminal and enter the following command:

./puppeth

[Genesis](https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/Genesis.JPG)

Type in a name for your network, like "puppernet" and hit enter to move forward in the wizard.

Leave this terminal for now...


### Creating Nodes

Copy and past the following into a new terminal to create the first node:
./geth account new --datadir node1

After this runs, you will be prompted to enter a password. Make sure to copy this password and the "Public Address of the Key" as seen in the following image.
![Node 1](https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/Node1.JPG)

Copy and paste the following into your terminal to create the second node:
./geth account new --datadir node2

Repeat the previous steps of entering a password and copying the password and "Public Address of the Key" for your records.


In order to initialize the first node with your genesis block, enter the following - don't forget to fill in your netwrk name from the genesis in step 1: 
./geth init yournetworkname.json --datadir node1

https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/3.JPG

Enter the following for your second node:
./geth init yournetworkname.json --datadir node2

https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/4.JPG

Return to the first terminal from the section on genesis, name your network, and select the option to configure a new genesis block.


### Proof of Authority

Return to the first terminal where the wizard is still open:
Type 2 to Manage existing genesis option
Type 2 to Export genesis scratch
Type 2 to choose Clique (Proof of Authority) consensus algorithm.

Paste both account addresses from the first step one at a time into the list of accounts to seal.

Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.

You can choose no for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.


Export genesis configurations. This will fail to create two of the files, but you only need networkname.json.

[json](https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/2.JPG)


Run the first node, unlock the account, enable mining, and the RPC flag. Only one node needs RPC enabled.


Set a different peer port for the second node and use the first node's enode address as the bootnode flag.

### When Node 1 Met Node 2
Enter the following command and immediately enter your password whether you can see the typing or not.
./geth --datadir node1 --mine --minerthreads 1

Scroll up while this is running and copy the entire "enode://" address

[Enode Address](https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/5b.JPG)

Go to another terminal and enter
./geth --datadir node2 --port 30304 --rpc --bootnodes "enode://<replace with node1 enode address>"
Make sure to replace what is within quotations with the enode address that you copied before.
You will need to enter the password immediately like you did before.

You should now see both nodes producing new blocks, congratulations!


### Send a Test Transaction

Use the MyCrypto GUI wallet to connect to the node with the exposed RPC port.

You will need to use a custom network, and include the chain ID, and use ETH as the currency.

Open up MyCrypto to get the private key of the ETH address you use to pre-fund your chain. Be sure the Kovan network is selected.

Unlock your wallet using your mnemonic phrase and choose the address you want to inspect.

Select the ETH address you use to pre-fund your chain, and in the "Select" dropdown list, choose Wallet Info.

Click on the eye icon next to the Private Key field, and copy and paste the private key of the wallet. Keep this handy, as you will use it in a bit.

Click "Add Custom Node", then add the custom network information that you set in the genesis.

[Custom Node](https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/7.JPG)

Make sure that you scroll down to choose Custom in the "Network" column to reveal more options like Chain ID:

Here is where you will send a test transaction to yourself.

Copy the pre-fund address into the "To Address" field, then fill in an arbitrary amount of ETH:

[Testing](https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/8.JPG)

Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.

[Confirmation](https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/9.JPG)

You should see the transaction go from Pending to Successful in around the same block time you set in the genesis.

[Status](https://github.com/ltayara1/Proof-of-Authority/blob/main/LT-Network/Screenshots/10.JPG)
