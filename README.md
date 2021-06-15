[![code style: achow](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/achow1o1)
<p><cd><p><a href="https://github.com/achow1o1/ASIC-Bitcoin-privatekey-Miner" rel="nofollow"><img src="https://camo.githubusercontent.com/0a47442b4a3342164618c1838f886fbbf2db735b585a8ba985b320318f0132bc/68747470733a2f2f696d672e736869656c64732e696f2f636f6465636f762f632f6769746875622f6477796c2f686170692d617574682d6a7774322e7376673f6d61784167653d32353932303030" alt="codecov.io " data-canonical-src="https://img.shields.io/codecov/c/github/dwyl/hapi-auth-jwt2.svg?maxAge=2592000" style="max-width:100%;"></a></p>

+ Firmware update  https://youtu.be/MHJ1ydIA3Go

+ NEW! Firmware (2020 Dec) S9, T9, S17, to S19Pro 
+ We only sell this file to 20 people. So far, we know 20 people who have.
+ ASIC-Bitcoin-privatekey-Miner
+ The sale is complete 

---------------------------------------------------------
+ Update 1.
+ NEW! Firmware (2021 Feb) S9, T9, S17,T19 to S19, S19Pro
+ We only sell this file to 20 people. So far, we know 20 people who have.
+ ASIC-Bitcoin-privatekey-Miner
+ The sale is complete

---------------------------------------------------------

+ Update 2.
+ NEW! Firmware (2021 April ) S9, T9, S17, T19 to S19 S19Pro
+ We only sell this file to 100 people. So far, we know 100 people who have.
+ + 24% another speed increase 
+ ASIC-Bitcoin-privatekey-Miner
+ Tutorial PDF & SETTING UP Included in .ZIP file

+ The sale is complete
---------------------------------------------------------
 
+ Update 3.
+ NEW! Firmware (2021 Junius ) SOON ! S9, T9, S17, T19 to S19 S19Pro
  
---------------------------------------------------------

+ NEW! Firmware !!!  SOON!! SOON!! 
+ Bitmain Antminer E9 3GH/s https://tinyurl.com/y6fw92w2
+ 265% another speed increase (32x RTX-3080)
+ Antminer E9 ASIC-Bitcoin-privatekey-Miner !
+ Tutorial PDF & SETTING UP Included in .ZIP file

---------------------------------------------------------

On this forum have repeatedly discussed ways to crack wallets in the Bitcoin blockchain. 
Typical hacking methods are key enumeration (LBC https://lbc.cryptoguru.org/about) and dictionary attack / brain wallets (https://eli5.eu/brainwallet/).
It is believed that breaking a wallet takes millions of years, but let me disagree. 
These calculations were done for household PCs.
In fact, there are only two bottlenecks. 
This is the key generation speed and the key verification speed.


Today, the mining chips make 71 Gh/s (BM1387). 
Bitfury Clarke is already 120 Gh/s. 
BM1391 produces 170-200 Gh/s, 1397 - already 440-500 Gh/s (in S17+). 
Do not forget that this is the speed of a double SHA-256 (SHA-256).
If we take the standard algorithm for addresses calculating (https://gobittest.appspot.com/Address) 
it is not difficult to notice that most of the steps are the same SHA-256 and SHA-256 (SHA-256). 
One RIPEMD-160 stage and several bit shifts. 
Is it possible to use the mining chip as a coprocessor when generating keys? Yes, 
it is possible, but more on that later.


The second bottleneck is checking the balance at the address found. The system should turn to the blockchain and make sure that there are bitcoins on the addresses belonging to the key pair. Compared to hashing speed, it is very slow.
The situation changes if you know a wallet or a private key with a balance. In this case, you should only verify a few bytes.


Armed with this knowledge, I assembled the simplest device based on the S9 hashboard and Cyclone IV FPGA evaboard. This works correctly and I was able to crack test wallets with a simple (low order) key.


Findings:
1. A hashboard is poorly suited for simultaneous computing. It is necessary to connect the chips in parallel, but not in a daisy chain.
2. It is necessary to organize the instruction pipelining in the FPGA for acceleration of calculations.


Now a little about the economy. Why is all this necessary?
I do not want to steal user funds. This is not possible in my system if your wallet is not generally known.
However, there are a lot of forgotten wallets in the blockchain. Some wallets contain thousands of bitcoins. And these wallets remain motionless for many years. You can consider this as a treasure, which has the right to change the owner, imho.


Take for example the Antminer S17e (64Th), whose current profitability is 0.5 btc/year.
The device contains 144 BM1397 chips with approximately 440 Gh at each.
We’ll make the calculation for a wallet protected by seed phrase with a 12-word. 
The English BIP39 dictionary contains 2048 words. 
With high probability the old wallet is encrypted in English (or Hex, lol).
((2048 ^ 12) / (144 * (440^9))) / (86400 * 365) = 1939618 years it will take one ASIC to search for all the combinations.
However, if we’ll track 10,000 wallets, then 1939618/10000 = 194 years to search for at least one match. 
And even if we have 100 ASICs, it turns out 2 years to search for at least one match (based on average luck).
These calculations are very simplified, but they show the order of numbers.


For 2 years, these same 100 ASICs will get 2*100*0.5 = 100 bitcoins. 
Provided there are no changes in the network’s hashrate and the power of ASICs (no).


At the same time, the difficulty of the seeds of abandoned wallets will never change.
And finding at least one wallet like 1FeexV6bAHb8ybZjqQMjJrcCrHGW9sb6uF 
can pay for the mining of 100 ASICs for 1600 years. 
Their name is Legion 12ib7dApVFvg82TXKycWBNpN8kFyiAN1dr, 
12tkqA9xSoowkzoERHMWNKsTey55YEBqkv, 
1PeizMg76Cf96nUQrYg8xuoZWLQozU5zGW etc.


Thus, mining abandoned addresses is more profitable than mining new coins. 
Over time, the situation will change in this direction IMHO.


A small calculation of effectiveness of using mining chips in bruteforce. 
Mining chips can greatly reduce the cost compared to FPGA-only solution.
S9 is capable of 14 TH/s (average). The main obstacle for bruteforce of HD wallets is 1.000.000 hashes. 
The chip does two hashes by default. In addition, it can load new data during hashing. 
Using cross-loading, this eliminates the load time losses. 
Thus, only 500.000 hashes need to be done without load time losses. 
How many wallets can hash this device? 2800 M.wallets/s. S17 Pro can hash 11200 M.w/s.

#(S17 Pro 585x faster than an RTX 3090)


In reality, the speed will be slightly lower because the hashboard is not designed to high speed communication 
(for maximum efficiency it is necessary to design ad hoc device). 
However, in just a few weeks many popular ASICs (T9/S9 etc) will become scrap. 
These are millions of free SHA-256 co-processors. 
Design a control board that can turn them into "seedpick" seems like a good idea.
ASIC's consumption will be halved (approximately) plus cascading to a pool. 
If you had a S9 farm this can be a powerful treasure hunt tool.


Let me remind I do not design a cracker. It will not be able to crack modern wallets. 
This is a forced restriction that I have programmed. 
If you have savings on old wallets (created until mid 2012 or started from "1"), just transfer BTC to modern ones and be safe. 
But abandoned wallets must be opened! As of January, out of the 18.14 million BTC 
that existed at that time, almost 60% had never moved.

--------------------------------------------------------

+ Resources for developers programmers, and software engineers !
+ ASIC Bitcoin Privatekey Miner Source Code !!
+ Support by email
+ Tutorial PDF & SETTING UP Included in .ZIP file
+ 30-day money back guarantee
+ https://satoshidisk.com/pay/CCLsLW


+ If you have any questions, write an Email: 
+ contact: achow@gmx.com


by
achow

