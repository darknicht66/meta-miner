# meta-miner
Meta Miner: allows to add algo switching support to *any* stratum miner.

Does not add any extra mining fees.

## Check mm.js builtin help

```
Usage: mm.js [<config_file.json>] [options]
Adding algo switching support to *any* stratum miner
<config_file.json> is file name of config file to load before parsing options (mm.json by default)
Config file and options should define at least one pool and miner:
Options:
        --pool=<pool> (-p):             <pool> is in pool_address:pool_port format, where pool_port can be <port_number> or ssl<port_number>
        --host=<hostname>:              defines host that will be used for miner connections (localhost 127.0.0.1 by default)
        --port=<number>:                defines port that will be used for miner connections (3333 by default)
        --user=<wallet> (-u):           <wallet> to use as pool user login (will be taken from the first miner otherwise)
        --pass=<miner_id>:              <miner_id> to use as pool pass login (will be taken from the first miner otherwise)
        --perf_<algo>=<hashrate>        Sets hashrate for algo that is: rx/0, rx/wow, cn/r, cn-pico/trtl, cn-heavy/xhv, cn/gpu, argon2/chukwa, k12, c29s, c29v, c29b, kawpow, ethash, autolykos2, panthera, ghostrider
        --algo_min_time=<seconds>       Sets <seconds> minimum time pool should keep our miner on one algo (0 default, set higher for starting miners)
        --miner=<command_line> (-m):    <command_line> to start smart miner that can report algo itself
        --<algo>=<command_line>:        <command_line> to start miner for <algo> that can not report it itself
        --watchdog=<seconds> (-w):      restart miner if is does not submit work for <seconds> (600 by default, 0 to disable)
        --hashrate_watchdog=<percent>:  restart miner if is hashrate dropped below <percent> value of of its expected hashrate (0 by default to disable)
        --miner_stdin:                  enables stdin (input) in miner
        --quiet (-q):                   do not show miner output during configuration and also less messages
        --verbose (-v):                 show more messages
        --debug:                        show pool and miner messages
        --log=<file_name>:              <file_name> of output log
        --no-config-save:               Do not save config file
        --help (-help,-h,-?):           Prints this help text
```

Check https://github.com/xmrig/xmrig-proxy/blob/master/doc/STRATUM_EXT.md#14-algorithm-names-and-variants for list of possible algo names.

## Sample mm.json (to use with xmrig v2.99.0+ located in the same directory)

```
{
 "miner_host": "127.0.0.1",
 "miner_port": 3333,
 "pools": [
  "gulf.moneroocean.stream:10001"
 ],
 "algos": {
  "cn/1": "./xmrig --config=config.json",
  "cn/2": "./xmrig --config=config.json",
  "cn/r": "./xmrig --config=config.json",
  "cn/fast": "./xmrig --config=config.json",
  "cn/half": "./xmrig --config=config.json",
  "cn/xao": "./xmrig --config=config.json",
  "cn/rto": "./xmrig --config=config.json",
  "cn/rwz": "./xmrig --config=config.json",
  "cn/zls": "./xmrig --config=config.json",
  "cn/double": "./xmrig --config=config.json",
  "cn/gpu": "./xmrig --config=config.json",
  "cn-heavy/0": "./xmrig --config=config.json",
  "cn-heavy/tube": "./xmrig --config=config.json",
  "cn-heavy/xhv": "./xmrig --config=config.json",
  "cn-pico": "./xmrig --config=config.json",
  "rx/0": "./xmrig --config=config.json",
  "rx/wow": "./xmrig --config=config.json",
  "rx/loki": "./xmrig --config=config.json",
  "rx/arq": "./xmrig --config=config.json",
  "rx/sfx": "./xmrig --config=config.json",
  "argon2/chukwa": "./xmrig --config=config.json",
  "argon2/wrkz": "./xmrig --config=config.json",
  "ghostrider": "./xmrig --config=config.json",
  "ethash": "./gminer/miner --server localhost:3333 --user 87MKQonkAUsQ9MNGKB3L51PE884cTeJbgcu6zWZPZt13b632huSGu9xPZwQALhLnAadEurYA8npRPZTJUWed95ZAT17brdt --pass gpu_miner --algo ethash --proto stratum",
  "kawpow": "./gminer/miner --server localhost:3333 --user 87MKQonkAUsQ9MNGKB3L51PE884cTeJbgcu6zWZPZt13b632huSGu9xPZwQALhLnAadEurYA8npRPZTJUWed95ZAT17brdt --pass gpu_miner --algo kawpow",
  "c29s": "./gminer/miner --server localhost:3333 --user 87MKQonkAUsQ9MNGKB3L51PE884cTeJbgcu6zWZPZt13b632huSGu9xPZwQALhLnAadEurYA8npRPZTJUWed95ZAT17brdt --pass gpu_miner --algo cuckaroo29s",
  "c29b": "./gminer/miner --server localhost:3333 --user 87MKQonkAUsQ9MNGKB3L51PE884cTeJbgcu6zWZPZt13b632huSGu9xPZwQALhLnAadEurYA8npRPZTJUWed95ZAT17brdt --pass gpu_miner --algo cuckaroo29b",
  "c29v": "./gminer39/miner --server localhost:3333 --user 87MKQonkAUsQ9MNGKB3L51PE884cTeJbgcu6zWZPZt13b632huSGu9xPZwQALhLnAadEurYA8npRPZTJUWed95ZAT17brdt --pass gpu_miner --algo cuckarood29",
  "autolykos2": "./trex/t-rex -a autolykos2 -o stratum+tcp://localhost:3333 -u 87MKQonkAUsQ9MNGKB3L51PE884cTeJbgcu6zWZPZt13b632huSGu9xPZwQALhLnAadEurYA8npRPZTJUWed95ZAT17brdt -p gpu_miner"
 },
 "algo_perf": {
  "rx/0": 243.6,
  "cn/r": 49.8,
  "cn/gpu": 12.9,
  "cn-heavy/xhv": 30.5,
  "cn-pico/trtl": 0,
  "rx/wow": 282.2,
  "defyx": 0,
  "argon2/chukwa": 4725.4,
  "k12": 0,
  "c29s": 0,
  "c29v": 0,
  "rx/loki": 243.6,
  "cn/0": 49.8,
  "cn/1": 49.8,
  "cn/2": 49.8,
  "cn/wow": 49.8,
  "cn/fast": 99.6,
  "cn/half": 99.6,
  "cn/xao": 49.8,
  "cn/rto": 49.8,
  "cn/rwz": 66.39999999999999,
  "cn/zls": 66.39999999999999,
  "cn/double": 24.9,
  "cn-heavy/0": 30.5,
  "cn-heavy/tube": 30.5,
  "c29b": 0.1865,
  "c29s": 0.23375,
  "c29v": 0.4875,
  "kawpow": 0.003953464329242706,
  "ethash": 49860000,
  "autolykos2": 144120000,
  "ghostrider": 1000
 },
 "algo_min_time": 0,
 "user": "89TxfrUmqJJcb1V124WsUzA78Xa3UYHt7Bg8RGMhXVeZYPN8cE5CZEk58Y1m23ZMLHN7wYeJ9da5n5MXharEjrm41hSnWHL",
 "pass": "x",
 "log_file": null,
 "watchdog": 600,
 "hashrate_watchdog": 0
}
```

## General configuration guidelines

* Configure your miners to connect to the single localhost:3333 (non SSL/TLS) pool.

* For best results separate xmr-stak/xmrig CPU and GPU miners (by using --noCPU, --noAMD, --noNVIDIA options for xmr-stak).

* Prepare your miner config files that give the best performance for your hardware on cryptonight, cryptonight-heavy, cryptonight-pico, randomx, randomx/wow, randomx/arq algorithm classes (not needed for xmrig v2.99+).

* If you have several miners on one host use mm.js --port option to assign them to different ports.

* Additional mm.js pools will be used as backup pools.

* To rerun benchmark for specific algorithm class use --perf_*algo*=0 option.

The configuration guide below is for stock xmrig. For xmr-stak/rx check [configuration guide for xmr-stak](xmr-stak.md) page.
For GPU mining setup using gminer algo check [configuration guide for gminer](gminer.md) page.
For c29 algo reference miner setup check [configuration guide for cuckaroo29](c29.md) page.

## Usage examples on Windows

Place mm.exe or mm.js (with nodejs installed) into unpacked miner directory either by:

* Download and unpack the latest mm-vX.X.zip from https://github.com/MoneroOcean/meta-miner/releases

* Download and install nodejs using https://nodejs.org/dist/v8.11.3/node-v8.11.3-x64.msi installator and download and unpack https://raw.githubusercontent.com/MoneroOcean/meta-miner/master/mm.js

### Usage example with xmrig on Windows

* Download and unpack the lastest xmrig-amd (https://github.com/xmrig/xmrig/releases/download/v5.4.0/xmrig-5.4.0-msvc-win64.zip).

* Modify config.json file in xmrig directory this way and adjust it for the best threads performance (out of scope of this guide):

	* Set "url" to "localhost:3333"
	* Set "user" to "89TxfrUmqJJcb1V124WsUzA78Xa3UYHt7Bg8RGMhXVeZYPN8cE5CZEk58Y1m23ZMLHN7wYeJ9da5n5MXharEjrm41hSnWHL" (put your Monero wallet address)

* Run Meta Miner (or use "node mm.js" instead of mm.exe):

```shell
mm.exe -p=gulf.moneroocean.stream:10001 -m="xmrig-amd.exe --config=config.json"
```

## Usage examples on Linux (Ubuntu 18.04)

Get node and Meta Miner (mm.js) in the miner directory:

```shell
sudo apt-get update
sudo apt-get install -y nodejs
wget https://raw.githubusercontent.com/MoneroOcean/meta-miner/master/mm.js
chmod +x mm.js
```

### Usage example with xmrig on Linux

* Get xmrig:

```shell
wget https://github.com/xmrig/xmrig/releases/download/v5.4.0/xmrig-5.4.0-xenial-x64.tar.gz
tar xf xmrig-5.4.0-xenial-x64.tar.gz
cd xmrig-5.4.0
```

* Prepare configs for different algorithms (put your Monero wallet address):

```shell
sed -i 's/"url": *"[^"]*",/"url": "localhost:3333",/' config.json
sed -i 's/"user": *"[^"]*",/"user": "89TxfrUmqJJcb1V124WsUzA78Xa3UYHt7Bg8RGMhXVeZYPN8cE5CZEk58Y1m23ZMLHN7wYeJ9da5n5MXharEjrm41hSnWHL",/' config.json
```

* Run Meta Miner:

```shell
./mm.js -p=gulf.moneroocean.stream:10001 -m="./xmrig --config=config.json"
```

## Developer Donations

If you'd like to make an one time donation, the addresses are as follows:

* XMR - ```89TxfrUmqJJcb1V124WsUzA78Xa3UYHt7Bg8RGMhXVeZYPN8cE5CZEk58Y1m23ZMLHN7wYeJ9da5n5MXharEjrm41hSnWHL```
* AEON - ```WmsEg3RuUKCcEvFBtXcqRnGYfiqGJLP1FGBYiNMgrcdUjZ8iMcUn2tdcz59T89inWr9Vae4APBNf7Bg2DReFP5jr23SQqaDMT```
* ETN - ```etnkQMp3Hmsay2p7uxokuHRKANrMDNASwQjDUgFb5L2sDM3jqUkYQPKBkooQFHVWBzEaZVzfzrXoETX6RbMEvg4R4csxfRHLo1```
* SUMO - ```Sumoo1DGS7c9LEKZNipsiDEqRzaUB3ws7YHfUiiZpx9SQDhdYGEEbZjRET26ewuYEWAZ8uKrz6vpUZkEVY7mDCZyGnQhkLpxKmy```
* GRFT - ```GACadqdXj5eNLnyNxvQ56wcmsmVCFLkHQKgtaQXNEE5zjMDJkWcMVju2aYtxbTnZgBboWYmHovuiH1Ahm4g2N5a7LuMQrpT```
* MSR - ```5hnMXUKArLDRue5tWsNpbmGLsLQibt23MEsV3VGwY6MGStYwfTqHkff4BgvziprTitbcDYYpFXw2rEgXeipsABTtEmcmnCK```
* LTHN - ```iz53aMEaKJ25zB8xku3FQK5VVvmu2v6DENnbGHRmn659jfrGWBH1beqAzEVYaKhTyMZcxLJAdaCW3Kof1DwTiTbp1DSqLae3e```
* WOW - ```Wo3yjV8UkwvbJDCB1Jy7vvXv3aaQu3K8YMG6tbY3Jo2KApfyf5RByZiBXy95bzmoR3AvPgNq6rHzm98LoHTkzjiA2dY7sqQMJ```
* XMV - ```XvyVfpAYp3zSuvdtoHgnDzMUf7GAeiumeUgVC7RTq6SfgtzGEzy4dUgfEEfD5adk1kN4dfVZdT3zZdgSD2xmVBs627Vwt2C3Ey```
* RYO - ```RYoLsi22qnoKYhnv1DwHBXcGe9QK6P9zmekwQnHdUAak7adFBK4i32wFTszivQ9wEPeugbXr2UD7tMd6ogf1dbHh76G5UszE7k1```
* XLA - ```SvkpUizij25ZGRHGb1c8ZTAHp3VyNFU3NQuQR1PtMyCqdpoZpaYAGMfG99z5guuoktY13nrhEerqYNKXvoxD7cUM1xA6Z5rRY```
* XHV - ```hvxyEmtbqs5TEk9U2tCxyfGx2dyGD1g8EBspdr3GivhPchkvnMHtpCR2fGLc5oEY42UGHVBMBANPge5QJ7BDXSMu1Ga2KFspQR```
* TUBE - ```TubedBNkgkTbd2CBmLQSwW58baJNghD9xdmctiRXjrW3dE8xpUcoXimY4J5UMrnUBrUDmfQrbxRYRX9s5tQe7pWYNF2QiAdH1Fh```
* LOKI - ```L6XqN6JDedz5Ub8KxpMYRCUoQCuyEA8EegEmeQsdP5FCNuXJavcrxPvLhpqY6emphGTYVrmAUVECsE9drafvY2hXUTJz6rW```
* TRTL - ```TRTLv2x2bac17cngo1r2wt3CaxN8ckoWHe2TX7dc8zW8Fc9dpmxAvhVX4u4zPjpv9WeALm2koBLF36REVvsLmeufZZ1Yx6uWkYG```
* XTNC - ```XtazhSxz1bbJLpT2JuiD2UWFUJYSFty5SVWuF6sy2w9v8pn69smkUxkTVCQc8NKCd6CBMNDGzgdPRYBKaHdbgZ5SNptVH1yPCTQ```
* IRD - ```ir3DHyB8Ub1aAHEewMeUxQ7b7tQdWa7VL8M5oXDPohS3Me4nhwvALXM4mym2kWg9VsceT75dm6XWiWF1K4zu8RVQ1HJD8Z3R9```
* ARQ - ```ar4Ha6ZQCkKRhkKQLfexv7VZQM2MhUmMmU9hmzswCPK4T3o2rbPKZM1GxEoYg4AFQsh57PsEets7sbpU958FAvxo2RkkTQ1gE```
* XWP - ```fh4MCJrakhWGoS6Meqp6UxGE1GNfAjKaRdPjW36rTffDiqvEq2HWEKZhrbYRw7XJb3CXxkjL3tcYGTT39m5qgjvk1ap4bVu1R```
* XEQ - ```Tvzp9tTmdGP9X8hCEw1Qzn18divQajJYTjR5HuUzHPKyLK5fzRt2X73FKBDzcnHMDJKdgsPhUDVrKHVcDJQVmLBg33NbkdjQb```
* XTA - ```ipN5cNhm7RXAGACP4ZXki4afT3iJ1A6Ka5U4cswE6fBPDcv8JpivurBj3vu1bXwPyb8KZEGsFUYMmToFG4N9V9G72X4WpAQ8L```
* DERO - ```dERokvcrnuWH1ai1QmZQc9cgxrLwE3rX3TbhdrnLmi3BVZmf197qd5FaFqmPMp5dZ3igXfVQwUUMgTSjpVKDtUeb6DT2xp64XJ```
* CCX - ```ccx7dmnBBoRPuVcpKJSAVZKdSDo9rc7HVijFbhG34jsXL3qiqfRwu7A5ecem44s2rngDd8y8N4QnYK6WR3mXAcAZ5iXun9BQBx```
* BLOC - ```abLoc5iUG4a6oAb2dqygxkS5M2uHWx16zHb9fUWMzpSEDwm6T7PSq2MLdHonWZ16CGfnJKRomq75aZyviTo6ZjHeYQMzNAEkjMg```
* RVN - ```RLVJv9rQNHzXS3Zn4JH8hfAHmm1LfECMxy```
* RTM - ```RUCyaEZxQu3Eure73XPQ57si813RYAMQKC```
* ERG - ```9fe533kUzAE57YfPP6o3nzsYMKN2W2uCxvg8KG8Vn5DDeJGetRw```
* BTC - ```3BzvMuLStA388kYZ9nudfm8L22937dSPS3```
* BCH - ```qrhww48p5s6zw9twhc7cujgwp7vym2k4vutem6f92p```
* ETH - ```0xCF8BABC074C487Ae17F9Ce0394eab492E6A35658```
* LTC - ```MCkjQo99VzoeZQ1piDzLDb4uqNSDRZpx55```
