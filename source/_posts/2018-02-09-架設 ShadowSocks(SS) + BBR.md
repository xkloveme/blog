---
title: 在 Google platform 上架設 ShadowSocks(SS) + BBR
tags:
  - 翻墙
date: 2018-02-09 07:06:00
---

### 建立 VPS

Google cloud platform 有免費 12 個月 300USD 的額度可以使用

- 註冊  [Google Clund Platform](https://cloud.google.com/)  服務
- 點擊左上角三條線漢堡，下拉選單到 「Compute Engine」 -> 「VM 執行個體」

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/ny3aKkXQTOOwP59kDLEB_E89EA2E5B995E5BFABE785A7202017-08-1220E4B88BE58D8811.54.09.png)

- 點擊 「建立執行個體」

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/1W8aYkspRQas9QXMs6O9_E89EA2E5B995E5BFABE785A7202017-08-1220E4B88BE58D8811.57.59.png)

**名稱**：自定義，這是你的機器名稱  
**區域**：請選 asia-east1-c 或是 asia-northeast1-b (亞洲區)  
**機器類型**：由於做個人翻牆工具，可以只選「微型」就好，規格選越高錢扣越快  
**開機磁碟**：請選作業系統 Ubuntu 14.04 LTS  
**防火牆**：將「允許 HTTP 流量」和「允許 HTTPS 流量」皆設為開啟

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/AR1NUHtmQvOzEatPQ0xA_E89EA2E5B995E5BFABE785A7202017-08-1320E4B88AE58D8812.04.53.png)

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/WOXE1PfhQYbUkCGIoQpG_E89EA2E5B995E5BFABE785A7202017-08-1320E4B88AE58D8812.06.21.png)

建立後，用瀏覽器打開 SSH 並輸入以下指令

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/PxSfuiYNTxC9dNeJYPxc_E89EA2E5B995E5BFABE785A7202017-08-1320E4B88AE58D8812.11.45.png)

每筆指令輸入後記得按 Enter

### 先安裝 BBR 加速

BBR 是  [Google 官方開源](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwj_he7Lj9LVAhVB2LwKHaLiAVEQFggnMAA&url=https%3A%2F%2Fgithub.com%2Fgoogle%2Fbbr&usg=AFQjCNGIK2TzybkL1laoWJd6BiRDTrRjOg)的擁塞算法來加速 TCP

也因為裝這個要重開機，所以先裝 XD

依序輸入

`wget –no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh`

`chmod +x bbr.sh`

`sudo ./bbr.sh`

輸入任意鍵執行

過程會需要一些時間約三分鐘，最後他會問你要不要重啟機器（Do you want to reboot?）輸入  `y`  同意

之後會斷開連線，請在重複之前打開這個視窗的動作「SSH」-> 「在瀏覽器視窗中開啟」

輸入  `sysctl net.ipv4.tcp_available_congestion_control`

如果有出現  `bbr`  字眼，就是安裝成功了

### 安裝 ShadowSocks(SS)

`sudo apt-get install python-pip -y`

`sudo pip install shadowsocks`

**重要！！！**  以下指令中的 password 請務必改成自己要使用的

`sudo ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start`

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/wwtPB5QjSm27fQdEUkWF_E89EA2E5B995E5BFABE785A7202017-08-1320E4B88AE58D8812.16.43.png)

將服務停止

`sudo ssserver -d stop`

再次運行

`sudo ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start`

大功告成，你已經有一台 SS + BBR 來做翻牆的機器了!

機器詳細資訊

- IP 位置是你架設機器在上面寫的「外部 IP」
- 密碼是剛剛你自行替換的「password」
- 加密規則是 aes-256-cfb
- port 通道 443

### 翻牆工具

我這邊是用 Surge ，不管手機跟電腦都是，要付費就是了，聽說也有免費的可以用，這部份就在[另一篇教程: **在 iphone 上透過 Shadowsocks(SS) 在大陸翻牆**](http://blog.niclin.tw/posts/2163079-wall-on-the-iphone-via-shadowsocks-ss-in-the-city-over-the-wall)講吧！

### 結果

這是用 surge 跑 benchmark 出來的結果，圖中的 GoogleTest 是邊敲本文章邊隨著架設的機器，可以看出速度還 OK

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/1Bm6YgbTHqmQAyHUUzI1_E89EA2E5B995E5BFABE785A7202017-08-1320E4B88AE58D8812.51.41.png)

Youtube 1080P Test

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/gJP7K5vCRi0V5ZJbmQiK_E89EA2E5B995E5BFABE785A7202017-08-1320E4B88AE58D8812.54.51.png)
