# houses_of_rome_neron_bot
This tool is intended to be used with [Houses Of Rome](https://romedao.finance/).   
It will optimize your sRome balance by claiming and autostaking automatically your pending bond rewards ~5min before each rebase.   
Also, it will automatically bond for you when a good discount opportunity is detected (5% by default).  
If a transaction fails in the process, Neron Bot will try to perform it with more gas (3 times max).  
It's Python, so you can run Neron Bot on almost all OS (as long as Python is installed, obviously). 

With Neron Bot, you'll never miss a great discount opportunity again, and you won't have to do all the tedious steps by hand to take advantage of it.

## Security
Private key is needed to sign all the transactions. I have absolutely no access to it, it will stay locally on your machine. That's why this tool is open source, so you can check by yourself by reading it that there's no need to worry. No security issues, no hidden fees !
## Features
### Automatic Rebase
- Claim and Autostake pending rewards for each bonds   
- 30 blocks (~=5min) before each ROME rebase   
### Automatic Bonding
- Available on FRAX bonds and ROME-FRAX LP bonds   
- Will use stacked ROME and / or pending rewards   
- Follows this pattern: claim pending rewards without autostaking, unstake ROME, swap ROME for FRAX, add liquidity (only if rome-frax lp discount) and bond.
### Logger
- Log each operation (bond / rebase) with their transactions in a json file.
## Settings
You can customize Neron Bot's behavior with the settings.json file.   
Here are the setting:   
- default_gas: 750000 by default
- default_gasprice: 2.5 by default
- min_bond_discount: 5 by default. The minimum discount percentage to trigger bonding process.
- min_srome_balance_to_bond: 0.2 by default. If you have less stacked rome than this amount, bonding process will not be triggered.
- min_pending_rewards_to_claim: 0.01 by default. The minimum pending reward amount (in a single bond contract) to trigger claims.
- use_pending_rewards: true by default. If you choose to use pending rewards, Neron will check if your stacked ROME balance + pending ROME rewards is greater than min_srome_balance_to_bond before bonding. If it's the case, it will claim without autostaking your pending rewards to use them for the bond.
## Installation
Install [Python 3](https://www.python.org/), then clone this repo:
```
git clone https://github.com/FlorianMgs/houses_of_rome_neron_bot.git
```
Move to the newly created folder:
```
cd houses_of_rome_neron_bot
```
Create a .env file following this template and fill it with your wallet address and private key:
```
WALLET_ADDRESS=your_wallet_address
PRIVATE_KEY=your_private_key
```
Then, you have to create a virtual environment:
```
python -m venv env
```
Activate it.
Windows:
```
env\scripts\activate.bat
```
Linux and macOS:
```
source env/bin/activate
```
Install required packages:
```
pip install -r requirements.txt
```
You can finally launch the script:
```
python main.py
```
## Heroku Deployment
You might want the bot to run 24/7 on the cloud. To do this, please signup to [Heroku](https://signup.heroku.com/).
Create a new app called "houses-of-rome-neron-bot".
Now you can deploy Neron Bot on Heroku:
```
heroku login
heroku git:remote -a houses-of-rome-neron-bot
git add .
git commit -m "Deployment commit"
git push heroku master 
```
Last step, you need to set your wallet address and private key as config vars:
```
heroku config:set WALLET_ADDRESS=your_wallet_address
heroku config:set PRIVATE_KEY=your_private_key
```
Now you're good to go, enjoy !!
## To Do List
- Automatically restack if a transaction fails more than 3 times in the bonding or rebase process. Currently, if it fails, you will end up with the last valid transaction resulted tokens in your wallet. Exemple, if bonding ROME for FRAX fails, you will end up with the swapped FRAX in your wallet, and have to manually bond them or swap them back for ROME.
- Add gOhm bonding support.
## Support
If you have any questions or suggestions about Houses of Rome Neron Bot, you can reach me out on Discord: Madgic#1963
## Donations
If you find this tool useful, feel free to send me a coffee! (any Metamask compatible network)      
0x8b85755F6D3D3B6f984F896b219f99BC561Ed057   
