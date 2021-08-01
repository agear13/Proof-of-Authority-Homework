# Proof-of-Authority-Homework

To set up a Proof of Authority Transaction, there are several things needed to set-up.
1. Anaconda
2. Web3 environment 
3. Mycrypto App
4. Go Ethereum (Recommend that you download the Geth & Tools from the 'Stable Releases'
5. Notepad (Note taking app such as Notepad on Windows)

Step 1: Create two wallets in MyCrypto. 

(1) Change your network to a test network such as Kovan (or any other Proof of Authority equivalent networks). You can find the button to change networks at the bottom of the left menu panel. 
(2) Create your wallet with a keystore file. ![screenshot mycrypto](https://user-images.githubusercontent.com/76278469/127755363-138f2a6c-24a3-4e16-badf-48b7fe685b4e.PNG)
This will allow you to store it in your local network. Ensure you save your password in a notepad! If you lose your password, you won't be able to access the wallet you've created! ![keystore screenshot](https://user-images.githubusercontent.com/76278469/127755386-c561079b-3bbf-4b25-8e9f-e308787f5c09.PNG)
To access your wallet after you've created it, you simply need to select view and send and the UTC file you've saved in your directory - then enter in your saved password. ![mycrypto screenshot](https://user-images.githubusercontent.com/76278469/127755395-63a13226-cd58-479b-8524-2824cee34672.PNG)
When you view your wallet, copy your public and private key and save it in your notepad containing your password - label it something easy that you'll remember such as 'Wallet 1'. 
Your notepad should look like:
Account 1
Public Key:
Private Key:
Password:
Repeat this process a second time to create your second wallet. Store the details in a seperate notepad. Your directory should then have two UTC addresses which unlock your two wallets. 

Step 2: Build your Genesis Block
Open your terminal and activate the ethereum environment with:
conda activate ethereum

Ensure you are working from the correct directory. E.g. if you have created a folder to store all relevant files called 'POA', change your directory to this with:
cd POA 

(1) Run the puppeth command with:
./puppeth

It will first ask what you'd like to call your network. Choose any name you like but again record this because you will need it later. 
Network name: flyingpigs

(2) Specify accounts to seal 

Next, it will ask what you would like to do?
Type 2, which instructs puppeth to configure a new genesis.

It will ask again, what would you like to do?
Type 1, which instructs puppeth to Create new genesis from scratch 

Next, it will ask what consensus engine to use?
Type 2, to choose Clique, proof of authority. 
![account screenshot](https://user-images.githubusercontent.com/76278469/127755525-5ae5726d-428c-406f-9962-a68b734f36ff.PNG)

It will then ask, how many seconds should blocks take?
Type 15 

Then, which accounts are allowed to seal?
Copy in your first wallet address WITHOUT THE OX. Press enter.
Copy in your second wallet address WITHOUT THE OX. Press enter.
Press enter again. 

It will then ask, which accounts should be pre-funded?
Type in your 2 wallet addresses again as above.

Then type yes to prefunding with wei. 

It will then ask what chain ID you want to set. Choose any 4 digit number. 
E.g 1234 (Record as you will need this)

Next, it will ask what would you like to do?
Type 2, to manage existing genesis. 

Then 2 again to export genesis configurations. 

It will then ask you what folder you'd like to save the genesis specs into?
Type in your relevant folder.

(3) Check that the specs are saved in your folder. 
Go to your folder in your local network and check that your network name folder is in there. There should be 2. A JSON file and a harmony file. 
E.g. flyingpigs.JSON & flyingpigs.harmony.
You can delete the harmony file as you won't need it. 


Now exit puppeth by hitting CTRL + C. 

Step 3: Build Nodes

(1) In your terminal, to create your first node, type:
./geth account new --datadir node1

It will ask you to enter a password, create a short one such as 'abc'. 

It will then generate a public address, path of the secret key file and password. 

Copy and paste these details into a seperate notepad and title it 'Node 1'. ![screenshot of node1 details](https://user-images.githubusercontent.com/76278469/127755644-d1dbf030-e8bb-455d-bde9-834779a9ab4a.PNG)

Repeat this for node 2 but change initial code to:
./geth account new --datadir node2.

(2) Initialise the Nodes
Type in the following command:
./geth init relevant_folder/network_name.json --datadir node1

E.g. 

./geth gen_files/zz.json --datadir node1

Then a second time for node 2.
![image](https://user-images.githubusercontent.com/76278469/127755714-4fc04c95-b5d3-493f-956e-39d53325af02.png)


./geth init relevant_folder/network_name.json --datadir node2

(3) Fire off the Nodes

In your same terminal, type in:

./geth --datadir node1 --unlock "FIRST_NODE_ADDRESS WITHOUT OX" --mine --rpc --allow-insecure-unlock

A prompt will come up for a password: Quickly enter your password for node1. It will then start looking for peers. Let this run. 

(3a) Then open up a new terminal. Enter in the following command after ensuring you've activated ethereum and are in the relevant folder:

./geth --datadir node2 --unlock "SECOND_NODE_ENODE_ADDRESS WITHOUT OX" --mine --port 30304 --bootnodes "encode://NODE_ONE_ENODE_ADDRESS@127.0.0.1:30303" -ipcdisable --allow-insecure-unlock

To get the SECOND NODE ADDRESS, you need to go to your first terminal, as your first node started running, scroll up to until you find a line starting with ENODE - copy that line until it the numbers 30303.

Then again, enter your password for your second node. 

Both nodes should now be running. 

![peer nodes screenshot](https://user-images.githubusercontent.com/76278469/127755810-e7920d6c-dd95-4ee7-a728-82701232d5c4.PNG)


(4) Send your transaction!

Open Mycrypto and change network - then add custom network. 

Type in the name of your node. Change network to Custom. 
Change Network name to your network name. Make currency ETH. Type in your chain ID that you saved earlier. 
Then make URL http://127.0.0.1:8545. 
Then click 'Save & Use Custom Node'. 

Then click 'View & Send', sign in with your keystore file as before.

Your wallet should show a huge account balance such as:
![money in wallet screenshot](https://user-images.githubusercontent.com/76278469/127755873-3667a6ed-1057-4b4b-80eb-541f7e8e2f08.PNG)

To send the transaction, paste the address of your second wallet WITH THE OX. 
Select a random number of ETH to send. Set transaction fee and then click send. A box will appear asking you to confirm the details of the transaction.
![send shot](https://user-images.githubusercontent.com/76278469/127755891-b3d3e328-9f4a-4d7a-b838-b7da15b97510.PNG)

Confirm, and you'll be able to see in your two terminal windows, the nodes sending the transaction. 

That's it! You've sent a transaction. 
