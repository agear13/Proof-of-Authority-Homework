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

In your terminal, to create your first node, type:
./geth account new --datadir node1

It will ask you to enter a password, create a short one such as 'abc'. 

It will then generate a public address, path of the secret key file and password. 

Copy and paste these details into a seperate notepad and title it 'Node 1'. ![screenshot of node1 details](https://user-images.githubusercontent.com/76278469/127755644-d1dbf030-e8bb-455d-bde9-834779a9ab4a.PNG)
