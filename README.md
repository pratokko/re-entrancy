 ## Re-Entrancy

 in our contract EtherStore is a contract where you can deposit and withdraw ETH.
 this contract is  vulnerable to re-entrancy attack lets see why

 1. deploy EtherStore
 2. Deposit one Ether each from Account 1 (Alice) and account 2 (Bob) into EtherStore
 3. Deploy Attack with the address of EtherStore
 4. Call Attack.attack  seinding one ether (using account 3(Eve)) you will get 3 ethers (2ethher stolen from Alice and Bob plus one ether sent from this contract)

 What happened?
 Attack  was able to call EtherStore.withdreaw multiple times before EtherStore.withdraw finished executing

 Here is how the functions were called
- Attack.attack
- EtherStore.deposit
- EtherStore.withdraw
- Attack fallback (receives 1 Ether)
- EtherStore.withdraw
- Attack.fallback (receives 1 Ether)
- EtherStore.withdraw
- Attack fallback (receives 1 Ether)