# Perfect on EC2 安裝筆記

在 2016 年底的時候, 有看到[一篇文章](https://medium.com/@rymcol/benchmarks-for-the-top-server-side-swift-frameworks-vs-node-js-24460cfe0beb)是目前 swift server 的一些評比分析如下圖

![](https://cdn-images-1.medium.com/max/2000/1*-J6071Zqsic7zY521MXUHg.png)

所以既然 `Perfect` 這麼厲害的話, 我們可以自己試著架設一台機器來玩看看. 按照目前的[兼容性](https://github.com/PerfectlySoft/Perfect#compatibility-with-swift), 目前支援為 `Swift 3.0.1`, 以這個為條件, 選擇架設的機器

## 首先要有一台開好的機器

以 `Swift 3.0.1` 這個條件去查 [swift.org](https://swift.org/download/#releases) 如下圖

![](https://s3-ap-northeast-1.amazonaws.com/daidoujiminecraft/Daidouji/%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7+2017-04-09+%E4%B8%8B%E5%8D%889.44.56.png)

我們可以選擇的 `Ubuntu` 版本有三種

 * 16.04
 * 15.10
 * 14.04
 
這邊我們選一個最新的版本 `16.04`

 * AMI - 這個時間點上, 最新的版本是 Ubuntu Server 16.04 LTS (HVM), SSD Volume Type - ami-1bfdb67c
 * Instance Type - t2.nano
 * Instance Details - 下一步
 * Add Storage - 下一步
 * Tag Instance - 下一步
 * Security Group - 預設 22 下一步

## 前置安裝

機器開起來後, 我們先在這台機器上面做一些基礎的更新, 以及一次安裝後面會用到的套件們

```
sudo apt-get update
sudo apt-get install clang openssl libssl-dev uuid-dev libcurl3 build-essential -y
```
 
## 安裝 Swift

以我們配置 `Ubuntu 16.04` + `Swift 3.0.1` 選擇相對應的下載

```
wget https://swift.org/builds/swift-3.0.1-release/ubuntu1604/swift-3.0.1-RELEASE/swift-3.0.1-RELEASE-ubuntu16.04.tar.gz
tar -xvzf swift-3.0.1-RELEASE-ubuntu16.04.tar.gz
export PATH=/home/ubuntu/swift-3.0.1-RELEASE-ubuntu16.04/usr/bin:$PATH
```

為了避免 export 每次都要重加, 可以使用 `sudo vi /etc/environment`, 將這個路徑加入, 內容如下

```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/home/ubuntu/swift-3.0.1-RELEASE-ubuntu16.04/usr/bin"
```

## 試用 PerfectTemplate

這邊官方有一個簡單的演示範例是 [PerfectTemplate](https://github.com/PerfectlySoft/PerfectTemplate), 可以架設一個簡單的 http service

```
git clone https://github.com/PerfectlySoft/PerfectTemplate.git
cd PerfectTemplate
swift build
```

build 好之後, 運行

```
.build/debug/PerfectTemplate
```

就可以在 8080 / 8181 跑起來囉~~~
