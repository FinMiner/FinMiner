# FinMiner by FINOM
# version: 2.2
**FinMiner** is a program product developed by the Finom company to create structural cryptocurrency units on the framework of the Ethash algorithm. The present version of **FinMiner** was made to work with every cryptocurrency based on this algorithm, including Ethereum, Ethereum Classic and many others. This version of **FinMiner** runs on Windows or Linux with AMD or Nvidia graphics cards.

In order to begin mining Ethereum with FinMiner, ***it's enough to simply input your wallet*** in the configuration file.

Testing on **FinMiner** demonstrated high performance working with Ethereum and Ethereum Classic. As a result of the research carried out, it was found that **FinMiner** performs on par with, and sometimes better than, competing program products. Independently of this, **FinMiner** stands out with its high stability and simple setup.
## Payment
Payment for the use of **FinMiner** takes the form of a commission from mining. The commission is 1% of total mining time: every hour at random **FinMiner** switches the mining to its wallets for 36 seconds.
## Setup
At launch **FinMiner** reads the _config.ini_ setup file from the program's current directory. When launching with the _-d_ command line option (e.g. `finminer.exe -d`) the miner displays a list of the devices it detects, including their PCI addresses and their amount of memory. In order to use this function on Windows the program must be launched from the command prompt (cmd).

**FinMiner** does not require any pools to be specified in the config file. If a pool (or list of pools) is not specified, **FinMiner** will automatically use the pools on [nanopool.org](https://nanopool.org/) corresponding to the chosen cryptocurrency.

When **FinMiner** starts up it displays the main work information in the console log, including the program’s current version, the name of the rig, the number and type of graphics cards installed and the program’s current settings.
## Log Files
The event log function on **FinMiner** is automatically activated each time the program starts up. The log files that are created contain all the information displayed on the console while the miner is running. By default, the log files are saved in the logs folder of the program's current directory. Deactivating event logging, as well as assigning a random catalogue for recording log files, can be done by using the corresponding configuration parameters (see the examples in the _Parameters_ section of this file).

## Remote Monitoring
**FinMiner** supports the network API program EthMan for rig monitoring. By default it opens port 3333 in “read-only” mode without the ability to restart the miner or rig through the network. In the program's config file, the port can be configured and the API function can be deactived with the _mport_ function. The config file also lets you set a password for monitoring with the _ethmanPassword_ option.

## Automatic Restart Function
With default settings, **FinMiner** will automatically restart if it encounters critical errors in the GPU or lag. (These errors usually arise due to hardware problems or overclocking the GPU.) The automatic restart function can be deactivated using the _watchdog_ parameter.

Likewise, the _minHashrate_ (minimum hashrate) parameter allows the user to set the value of the minimum hashrate which, if exceeded, will cause the miner to restart. This function uses the average hashrate over the last ten minutes, as displayed in blue in the console log. If the average hashrate over 10 minutes is lower than the set value, the miner will restart. With default settings the minimum hashrate is not set.

Another function on **FinMiner** that improves the miner's automatic functioning is handled by the _restarts_ parameter.It sets the number of times the miner restarts before rebooting the worker (rig). By default the miner will only restart itself.

More detailed information on using these functions can be found in the _Parameters_ section of this file.

## Parameters
The settings for **FinMiner** can be found in the configuration file _config.ini_ in the .ini format as _parameter=value_ logic pairs. This file permits the presence of empty lines and comments. Comment lines should begin with a ";" (semicolon). The parameters and values are not case-sensitive, which means it makes no difference to the program whether you type _ETH_, _eth_ or _Eth_, or whether you type _wallet_ or _Wallet_. If an incorrect value is set for a parameter, the default value will be used instead (note that this rule does not apply to the _wallet_ parameter).

What follows is a list of the parameters that can be set on **FinMiner**.
### wallet
Mandatory parameter.
This is the user's wallet, where funds will be deposited.
### coin
Optional parameter.
This chooses the default coin for the pool. The default pool is [nanopool.org](https://nanopool.org/).
The coin parameter accepts one of two values: ETH (for Ethereum) and ETC (for Ethereum Classic). When a coin is specified  **FinMiner** automatically determines the pool necessary for it to function if none have been provided in a separate parameter. If a coin is not specified, **FinMiner** will use the default coin Ethereum. Moreover, if [nanopool.org](https://nanopool.org/) is specified in the configuration file for Ethereum or Ethereum Classic, **FinMiner** can determine the coin from the pool's settings.

*Important*: when using **FinMiner** to mine Ethereum Classic on the default pool, it is necessary to define the coin (coin=ETC). In that case the pools will be determined automatically.

If the pools are clearly defined with the aid of the _pool1, pool2, ..._, parameters, then **FinMiner** will function according to the tasks it receives from those pools.
### rigName
Optional parameter.
This is the name of the rig (computer/worker). It will be displayed in the pool's statistics. If this parameter is not set, the program will generate a unique name and provide it to the pool.
### email
Optional parameter.
This is the user’s e-mail address. It is provided to the pool where the rig will be operating. The pool can use it when sending out service notifications.
### pool1, pool2, ...
Optional parameter.
This defines the set of mining pools used. Values must be given in the format url:port (e.g. `pool1=eth-eu1.nanopool.org:9999`). The parameters should be defined in ascending, sequential order, from pool1 to poolN (for example: pool1, pool2, pool3). The pool will be chosen automatically from the list in accordance with the maximum connection speed. If the pool (or list of pools) is not defined, **FinMiner** will automatically use the pools on [nanopool.org](https://nanopool.org/) that correspond to the chosen cryptocurrency.
### rigPassword
Optional parameter.
The password for the rig (or worker). It may be necessary when working with pools that require registration and setting a rig password.
### watchdog
Optional parameter.
This parameter manages the miner's restart function when running into critical GPU errors or lag. It accepts the values _true_ or _false_. By default, _true_ – automatic restart - is activated.
### minHashrate
Optional parameter.
This is the minimum acceptable hashrate. This function keeps track of the rig's total hashrate and compares it with this parameter. If five minutes after the miner is launched the set minimum is not reached, **FinMiner** will automatically restart. Likewise, the miner will restart if for any reason the average hashrate over a ten-minute period falls below the set value. This value can be set with an optional modifier letter that represents a thousand for kilohash or a million for megahash per second. For example, setting the value to 100 megahashes per second can be written as 100M, 100.0M, 100m, 100000k, 100000K or 100000000. If this parameter is not defined, the miner will not restart (with the exception of the situations described in the _watchdog_ section).
### devices
Optional paramter.
These are the graphics cards that will be used by the miner. If you do not want to launch the miner on all available GPUs but only on some of them, their numbers can be provided in the _devices_ parameter separated by a comma. **FinMiner** numbers the GPUs starting from zero in ascending order of their PCI addresses. You can see a list of available GPUs and the order in which they're in by launching **FinMiner** with the _-d_ command line option:
```
finminer -d
```
For example, if there are four GPUs in the system (0, 1, 2, 3) and all but the second-to-last one (indexed as 2) must be set to mine, then the devices option must be set in the following manner:
```
devices=0,1,3
```
The order of devices determines the order of displayed hashrate. For example, if it is set as
```
devices=3,1,0
``` 
then the hashrate line will first display GPU3, then GPU1 and finally GPU0.

### restarts
Optional parameter.
This parameter sets the number of times the miner will restart before rebooting the rig. In case of GPU problems like hardware errors or lag, or in case of hashrate degradation (if the _minhashrate_ option is used), **FinMiner** will restart. However, certain errors cannot be fixed by restarting the program. In such cases it is necessary to reboot the rig. To reboot, the miner loads the _reboot.bat_ script from the current directory if running on Windows or _reboot.sh_ if on Linux:
```
reboot
```
The typical content of the _reboot.bat_ script for Windows:
```
shutdown /r /t 5 /f
```
The script must be written by the user.

### noLog
Optional parameter.
This parameter accepts the values _true_ or _false_ (the default is _false_). If this parameter is set to _true_ then no log files will be recorded onto the hard drive.

### logDir
Optional parameter.
This is the name of the folder in which log files will be created. The default destination is _logs/_.

### mport
Optional parameter.
This is the network port for remote monitoring and program management through EthMan or other programs that use a similar API protocol format.
The program supports all API functions, including restarting the miner and rig(s).
You can block miner management through API (in which case the miner will only display the statistics and won't respond to any commands). To enable this function, a "minus" (-) sign must be written before the port number.
And you can completely deactivate remote monitoring. To do this, the port number must be set to "0" (zero).
Default value: -3333 (This means that the miner blocks management through API and displays statistics on port 3333).

### ethmanPassword
Optional parameter.
Your password for monitoring with EthMan and other utilities that support the same network API.

## Configuration File
The minimum configuration file for Ethereum may contain only a wallet:
```
wallet=<wallet>
```
**FinMiner** will automatically use Ethereum pools.

To work with Ethereum Classic, the coin must be specified:
```
wallet=<wallet>
coin=ETC
```
In this case **FinMiner** will use pools corresponding to Ethereum Classic.

## IMPORTANT!
For coins that run on the Ethash algorithm but are not supported by [nanopool.org](https://nanopool.org/), **you must** specify a **wallet** and pools (**pool1...**). In this case **FinMiner** will function as if it were working with Ethereum,  but the results of its operations will be determined by tasks from the corresponding pools specified in the configuration file.

## Examples of Configuration Files
Example of a configuration file for Ethereum:
```
wallet = 0xffffffffffffffffffffffffffffffffffffffff
rigName = rig1
email = someemail@org
pool1 = eth-eu1.nanopool.org:9999
pool2 = eth-eu2.nanopool.org:9999
pool3 = eth-us-east1.nanopool.org:9999
pool4 = eth-us-west1.nanopool.org:9999
pool5 = eth-asia1.nanopool.org:9999
pool6 = eth-jp1.nanopool.org:9999
pool7 = eth-au1.nanopool.org:9999
```
Example of an equivalent file for Ethereum:
```
wallet = 0xffffffffffffffffffffffffffffffffffffffff
rigName = rig1
email = someemail@org
```
Example of a minimum file for Ethereum:
```
wallet=0xffffffffffffffffffffffffffffffffffffffff
```
Example of a configuration file for Ethereum Classic:
```
wallet = 0xffffffffffffffffffffffffffffffffffffffff
coin=Etc
rigName = rig1
email = someemail@org
pool1 = etc-eu1.nanopool.org:19999
pool2 = etc-eu2.nanopool.org:19999
pool3 = etc-us-east1.nanopool.org:19999
pool4 = etc-us-west1.nanopool.org:19999
pool5 = etc-asia1.nanopool.org:19999
pool6 = etc-jp1.nanopool.org:19999
pool7 = etc-au1.nanopool.org:19999
```
Example of an equivalent file for Ethereum Classic:
```
wallet = 0xffffffffffffffffffffffffffffffffffffffff
coin=Etc
rigName = rig1
email = someemail@org
```
Example of a minimum file for Ethereum Classic:
```
wallet=0xffffffffffffffffffffffffffffffffffffffff
coin=Etc
```
