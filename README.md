# آموزش ران کردن نود بیس Base
![image](https://iili.io/HXNL4YN.jpg)


<h1 align="center"> Base Node Install guide in Persian </h1>
<h1 align="center"> راهنمای نصب نود بیس به فارسی <br> 👽 Moeendoteth 👽
</h1>

## 👽  اطلاعات و نیازمندی ها

درحال حاضر برنامه تشویقی برای ران کردن نود بیس وجود نداره، ولی با توجه به اینکه مربوط به کوین بیس هست، فکر می کنم مهم باشه 

### لینک های من
 * [Moeen's Twitter](https://twitter.com/Moeendoteth)
* [Moeen's Lens](https://lenster.xyz/u/moeen)
 
 ## 👽  مشخصات پیشنهادی

- 16 GB RAM
- 100 GB SSD

دستورهای مراحل نصب رو اینجا میزارم
اگر VPS ندارید من از هتزنر خریدم و با لینک زیر میتونید ۲۰یورو اعتبار مجانی کسب کنید:


 * [Hetzner](https://hetzner.cloud/?ref=p7amgYr2ILM7)

## به روزرسانی لینوکس
 
```shell
sudo apt update
```

```shell
sudo apt upgrade
```


## 👽  نصب داکر Docker

```shell
apt install docker-compose
```

```shell

sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin

```
<br><br>

#### 👽. کلون کردن فایل های گیتهاب بیس.

```
git clone https://github.com/base-org/node.git
```

#### 👽  ایجاد صفحه جدید 
```
screen -S base
```

#### 👽  وارد پوشه ای که برای بیس ساختیم میشیم

```
cd node
```

#### 👽 . توی این مرحله باید فایل کامپوز رو ادیت کنیم

برای این مرحله شما به داشتن یک RPC روی اتریوم گورلی نیاز دارید، اگر ندارید میتونید با آلکمی یکی بسازید


* [Alchemy](https://alchemy.com/?r=jk4ODk2NDUwNzU5N)

اگر احتیاج به آموزش ساخت RPC هم دارید چند مرحله لینک زیر میتونه بهتون کمک کنه،
فقط حواستون باشه باید 
ETH - Goerli 
بسازید

https://mirror.xyz/blog.persiandao.eth/WAXjgu57BDTyohyGecaNEaxL0XpvoFTv3ELRQhf5wbU

بعد از این مراحل و داشتن لینک RPC یعنی همون لینکی که با https شروع میشه

ویرایشگر نانو رو باز کنید

```
nano docker-compose.yml
```

<br><br>
باید قسمت خاکستری خط رو ویرایش کنید : 
OP_NODE_L1_ETH_RPC=`https://ethereum-goerli-rpc.allthatnode.com`
<br>
لینک RPC رو به جای اون قسمت مشخص شده پیست کنید و بعد از اون 
ctrl + x رو همزمان بزنید
سوالی که ازتون میپرسه رو y بزنید و اینتر


![image](https://iili.io/HXNrb4I.png)



####👽 حالا باید نود رو راه اندازی کنیم

<br>

برای این مرحله باید صبور باشید، کمی زمان خواهد برد <br>

```
docker compose up
```

وقتی تموم بشه، یه همچین صفحه ای باید ببینید
![image](https://iili.io/HXO22wv.png)

<br>

#### 👽  دستورات دیگه

بعد از اینکه داکر شما کامپوز شد، میتونید با اجرای این دستور در روت دایرکتوری node
همچین خروجی بگیرید

```
curl -d '{"id":0,"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest",false]}' \
  -H "Content-Type: application/json" http://localhost:8545
```
![image](https://iili.io/HXN4WnR.png)

<br>


همچنین برای چک کردن وضعیت سینک نود خودتون میتونید از دستور زیر استفاده کنید

```
echo Latest synced block behind by: \
$((($( date +%s )-\
$( curl -s -d '{"id":0,"jsonrpc":"2.0","method":"optimism_syncStatus"}' -H "Content-Type: application/json" http://localhost:7545 |
   jq -r .result.unsafe_l2.timestamp))/60)) minutes
```


ممنون میشم اگر این مطلب رو ستاره بدید
