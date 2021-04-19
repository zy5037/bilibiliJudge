# 风纪委员会自动投票

## Docker分支 

本分支为Docker版，使用Docker-Compose部署即可！

本脚本通过使用Github Action来实现B站风纪委员的自动投票功能，喜欢请给我点个STAR吧！

如果你不是风纪委员，在符合风纪委员申请条件的情况下，本脚本会自动帮你申请

投票时间是早上八点，如果有需要请自行修改`.github/workflows/Judge.yml`中的时间，时间是UTC时区的时间，需要将时位+8才是北京时间

**使用本脚本即代表你放弃追究开发者任何由使用本脚本而造成的责任，所有的责任由使用者自行承担！**

## 赞助
点击下面的Badge其中一个就可以跳转到相应页面，感谢老板的支持！

<a href="https://afdian.net/@GamerNoTitle"><img src="https://img.shields.io/badge/%E7%88%B1%E5%8F%91%E7%94%B5-GamerNoTitle-%238e8cd8?style=for-the-badge" alt="前往爱发电赞助" width=auto height=auto border="0" /></a> <a href="https://cdn.jsdelivr.net/gh/GamerNoTitle/Picture-repo@master/img/Donate/WeChatPay.png"><img src="https://img.shields.io/badge/%E5%BE%AE%E4%BF%A1%E6%94%AF%E4%BB%98-GamerNoTitle-%2304BE02?style=for-the-badge" alt="使用微信赞助" width=auto height=auto border="0" /></a> <a href="https://cdn.jsdelivr.net/gh/GamerNoTitle/Picture-repo@master/img/Donate/AliPay.jpg"><img src="https://img.shields.io/badge/%E6%94%AF%E4%BB%98%E5%AE%9D%E6%94%AF%E4%BB%98-GamerNoTitle-%231678FF?style=for-the-badge" alt="使用支付宝赞助" width=auto height=auto border="0" /></a>

## 目录

- [使用方法](#使用方法)
- [变量获取](#变量获取)
    - [csrf与sessdata](#csrf与sessdata)
    - [giveup与delay](#giveup与delay)
    - [JudgeProportion](#JudgeProportion)
- [免责声明](#免责声明)

## 从零开始的使用指北☞

### 使用方法

1、Fork本仓库，直接点击右上角的Fork图标，然后将项目选择到你的账户下即可

![](https://upimage.alexhchu.com/2021/01/26/55beb284a6a45.png)

2、进入设置，添加变量必需变量`csrf`和`sessdata`，另有`giveup`和`delay`可选变量可以添加

**请注意：你无需在仓库的secrets内设置名为`GITHUB_TOKEN`的变量，该名称本身就是指定为自己账户下名为`GITHUB_TOKEN`的密钥，如果你在仓库的secrets内设置将会被Github提示无效**

[如何获取变量内容？请点这里](#变量获取)

![](https://upimage.alexhchu.com/2021/01/26/404fb80a80b5a.png)

![](https://upimage.alexhchu.com/2021/01/26/b2d3f92a2a9c3.png)

### 变量获取

#### csrf与sessdata

首先我们打开B站，直接在B站的网址后面加上`/judgement`，或者直接访问[https://bilibili.com/judgement](https://bilibili.com/judgement)，按下键盘上的<kbd>F12</kbd>，打开开发者工具

接着我们点到上面的`Network`（有些写的是`网络`，例如Edge），在左边找到index项，然后点击它，在右侧找到cookie这一个键，然后复制`SESSDATA=`到`;`的内容作为`sessdata`和`bili_jct=`到`;`的内容作为csrf

**请注意：不要把分号弄进去了！不要分号！不要分号！（重要的事情说三遍）**

![](https://upimage.alexhchu.com/2021/01/26/a892c4e380db5.png)

#### giveup与delay

这是两个我设定的值，因为B站对于案件有`放弃`这一说，所以我对它特别加了个开关

如果你不想让脚本对案件采用放弃的操作，那么就要添加Giveup这个值，而且必须填上`False`，否则一律当允许放弃处理；还有一个delay是不放弃的话等待多长时间以后再次进行操作计算，以秒为单位，必须是整数，不填就默认为`300`秒

#### JudgeProportion

这是一个设定赞成比例的值，默认设定的是0.7，即赞成票占全部的70%就选择赞成中票数较高的操作，或合规票占全部的70%（即违规占30%）时就投合规，否则进入放弃/等待阶段，这个数字必须是大于0且小于1的小数！若输入无效数字按默认值处理！

## 免责声明

学习项目，请勿滥用！如果有因滥用造成的封号、删除账户等情况或违反相关法律所造成的责任，本人拒不承担！

