# blockchain-homework
Creating a Genesis Block
In this activity, you will create your genesis block using puppeth, a tool bundled with the Go Ethereum tool.
The genesis block is the first step towards creating your very own new blockchain!
If you have not yet installed the Go Ethereum tool, or if you have any issues, please refer to the Unit 18 Installation Guide for help.
Recall that by terminal window, we refer to the Terminal in Mac, or Git Bash in Windows.

Instructions

Open a terminal window, navigate to the Blockchain-Tools folder and type the following command:

./puppeth

This should show the following prompt:

![image](https://user-images.githubusercontent.com/84012921/133360838-e0c51be8-f197-4437-8f52-0cbbdf1e3925.png)



Type in a name for your network, like "puppernet" and hit enter to move forward in the wizard.


Type 2 to pick the Configure new genesis option, then 1 to Create new genesis from scratch:

![image](https://user-images.githubusercontent.com/84012921/133360852-7d041ce3-9fa1-4bd8-baed-e13e9f0ec4dc.png)


Now you have the option to pick a consensus engine (algorithm) to use.

Type 1 to choose Proof of Work and continue.

You will be asked to enter a pre-fund account.


Copy and paste an address from your Ethereum wallet in MyCrypto, without the 0x prefix.


Once you paste an address and hit enter, hit enter again on the blank 0x address to continue the prompt.


Continue with the default option for the prompt that asks Should the precompile-addresses (0x1 .. 0xff) be pre-funded with 1 wei? by hitting enter again,
until you reach the Chain ID prompt.

![image](https://user-images.githubusercontent.com/84012921/133360868-99a05a4f-4ccd-4856-97f6-fb9c3730178c.png)



Come up with a number to use as a chain ID (e.g. 333) type it, then hit enter.

You should see a success message and be redirected to the original prompt:

![image](https://user-images.githubusercontent.com/84012921/133360877-cf62eca6-fbf7-4215-8376-6f9e846444e3.png)


Awesome! Your genesis configuration is stored in your local home directory.
We'll export this later. For now, congratulate yourself on creating the rules for your new blockchain network!



Creating two nodes with accounts
In this activity, you will create two accounts for nodes to use for mining rewards.
Then, you will initialize the nodes using the genesis block configuration you created earlier to prepare them for bringing the chain to life!

Instructions
First, export your genesis configuration into a yournetworkname.json file as follows:


In the puppeth prompt, navigate to the Manage existing genesis by typing 2 and hitting enter.


You may have to type your network name again first if you're launching puppeth fresh.


Then, type 2 again to choose the Export genesis configurations option, and continue with the default (current) directory by hitting enter:

![image](https://user-images.githubusercontent.com/84012921/133360962-dce35cf3-d360-49ed-a3b5-35159109ab9e.png)



This will export several yournetworkname.json files -- we will only be using the first one without aleth, parity, or harmony suffixes.

Now, we need to create at least two nodes to build the chain from the genesis block onward:


Exit puppeth by using the Ctrl+C keys combination.


Create the first node's data directory using the geth command and a couple of command line flags by running the following line in your terminal window (Git Bash in Windows):


./geth account new --datadir node1
You should see a success message similar to this one:

![image](https://user-images.githubusercontent.com/84012921/133360975-3ccc0745-838e-4c5b-bcd3-9125f2f9c965.png)


Create a new text file for notes, and copy the node's address into the file and label it Node 1 Key.


Repeat the same process for the second node by replacing the datadir parameter with the node2 folder.


./geth account new --datadir node2

Make sure to keep track of the node's addresses and which belongs to which.

Now, it's time to initialize and tell the nodes to use your genesis block!

Initialize the first node, replacing yournetworkname.json with your own:

./geth init yournetworkname.json --datadir node1
You should see this success message:

![image](https://user-images.githubusercontent.com/84012921/133361047-e5a0c1dc-8c53-411b-bf90-786cba3477ea.png)


Since you only initialize your nodes once, you don't need to copy anything into your notes here.


Run the same command for node2.


./geth init yournetworkname.json --datadir node2
Get excited, because your blockchain is only a couple steps away from being brought to life!

![image](https://user-images.githubusercontent.com/84012921/133356601-77659c48-5986-4be8-85d8-7233ee38a548.png)

Bringing your blockchain to life
In this activity, you will start both previously created nodes to bring your blockchain to life.


node1 will be a full node that is also mining.


node2 will be a full node that exposes an RPC port, allowing you to talk to it with other apps like MyCrypto.



Instructions
Time to start your blockchain network! Open a terminal window (Git Bash in Windows) navigate to your Blockchain-Tools folder and follow the next steps.
In your notes text file, make sure to keep track of every command you run in this activity for later. You can use these notes as a cheat-sheet later to easily start your chain again.

Launch the first node into mining mode with the following command:

./geth --datadir node1 --mine --minerthreads 1


The --mine flag tells the node to mine new blocks.


The --minerthreads flag tells geth how many CPU threads, or "workers" to use during mining. Since our difficulty is low, we can set it to 1.


You should see the node Committing new mining work:

![image](https://user-images.githubusercontent.com/84012921/133361268-f7d9b04b-47cf-46d3-8b9c-dc4e5e741aec.png)


Copy this command into your notes and label it Start Node 1.

Now you will launch the second node and configure it to let us talk to the chain via RPC.

Scroll up in the terminal window where node1 is running, and copy the entire enode:// address (including the last @address:port segment) of the first node located in the Started P2P Networking line:


![image](https://user-images.githubusercontent.com/84012921/133361286-71676a5c-41a0-45a6-9b50-a363b44ddd6b.png)



We will need this address to tell the second node where to find the first node.


Open another terminal window and navigate to the same directory as before.


Launch the second node, enable RPC, change the sync port, and pass the enode:// address of the first node in quotes by running the following command (it will differ in Windows and OS X):


Running in OS X:


./geth --datadir node2 --port 30304 --rpc --bootnodes "enode://<replace with node1 enode address>"

Running in Microsoft Windows:

./geth --datadir node2 --port 30304 --rpc --bootnodes "enode://<replace with node1 enode address>" --ipcdisable

The output of the second node should show information about Importing block segments and synchronization:

![image](https://user-images.githubusercontent.com/84012921/133361306-7763b00f-3fbe-4011-bc21-e58c92ab53f7.png)

