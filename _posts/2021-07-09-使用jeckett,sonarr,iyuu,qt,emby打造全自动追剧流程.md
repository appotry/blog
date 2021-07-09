---
layout: post
title: 使用jeckett,sonarr,iyuu,qt,emby打造全自动追剧流程
date: 2021-3-03
categories: [Docker, PT]
tags: [Docker, PT, Emby, Sonarr, Jeckett, Portainer, Watchtower]
description: 使用jeckett,sonarr,iyuu,qt,emby打造全自动追剧流程。

image:
  src: https://p.sda1.dev/2/d70275e65c9233ac67b92234f1b0ddca/Snipaste_2021-07-09_13-03-59.png
  width: 1000   # in pixels
  height: 400   # in pixels
  alt: image alternative text
---

注意：图床使用sda1，图片显示问题自己解决

jackett 作为种子源，sonarr剧集管理，bt下载，qbittorrent主力下载，使用iyuu转移辅种，emby，jellyfin做海报墙。基本算是完美打通全流程自动追剧。bt种子文件命名规则SxxExx的自动识别下载，国内的资源手动查找下载，自动推送到emby刮削好

硬链接工具导入到新目录，使用TMM刮削

## sonarr管理剧集名，查找剧集种子推送到下载工具

剧集管理示例图片

管理剧集目录，剧集日历，提醒你那一天哪些节目播放

![img](https://p.sda1.dev/2/d70275e65c9233ac67b92234f1b0ddca/Snipaste_2021-07-09_13-03-59.png)



![img](https://p.sda1.dev/2/8810a4240ef4fa1bf7b3be33db51d4dd/Snipaste_2021-07-09_13-00-29.png)

自动识别下载对英文剧集支持较好，对于中文资源，结合手动识别下载更佳。

### 手动识别下载

示例图片

![img](https://p.sda1.dev/2/c549d493aefe49bf98477dcb3a51200b/Snipaste_2021-07-09_13-03-15.png)

## **emby海报墙，流媒体中心**

emby作为海报墙，元数据查看器，结合tampermonkey js脚本调用外部potplayer播放减少nas服务器压力，并且得到更好解码性能。手机端也有emby客户端。jellyfin，plex也可以

js脚本: [embyLaunchPotplayer](https://greasyfork.org/scripts/406811-embylaunchpotplayer/code/embyLaunchPotplayer.user.js)



![img](https://p.sda1.dev/2/dafba673fa2978cd2cf25278c789e10a/Snipaste_2021-07-09_13-02-19.png)



![img](https://p.sda1.dev/2/aea2d8b666d1a990b14f3ccd60486121/Snipaste_2021-07-09_13-13-39.png)

## **tmm刮削，改名**

一些命名不规范，不能被emby识别的剧集使用tmm刮削改名，配合硬链接工具，可以不影响做种的前提下改名，该目录。大文件硬链接，小文件直接复制方便刮削，推荐一个自己写的硬链接bash shell脚本

<https://github.com/appotry/PTtool>，PTtool在nas，linux环境使用更方便



![img](https://p.sda1.dev/2/20ae181bced25779288dd384868bb375/Snipaste_2021-07-09_13-17-52.png)



 

电影使用radarr, 音乐使用lidarr，同样可以自动化过程

## 使用radarr管理电影

radarr示例图片![img](https://p.sda1.dev/2/fc00cb088322ae3c450bf8c5168a931a/Snipaste_2021-07-09_13-30-01.png)

## 使用lidarr管理音乐

lidarr示例图片
![img](https://p.sda1.dev/2/8ec9ac307484c88de0fec74a13cfcc58/Snipaste_2021-07-09_13-30-40.png)

 

### 使用docker compose 管理docker配置文件，一键安装，升级

## 使用portainer管理docker

![img](https://p.sda1.dev/2/735dcefd82d5a6e8460f3636ca7c6a25/Snipaste_2021-07-09_13-35-10.png)

## 使用watchtower自动升级docker

使所有软件保持最新最佳状态

![img](https://p.sda1.dev/2/c509f2cdae0fdde67e1d4ffac8e46a0a/watchtower.png)



## 使用muximux来管理多个docker入口

主页面

![](https://p.sda1.dev/2/fcf3217ebb36504ad4d7030a7394432f/Snipaste_2021-07-09_14-13-06.png)



配置页面

![img](https://p.sda1.dev/2/a223e8ae492f13e9984af7553f06c681/Snipaste_2021-07-09_14-13-50.png)



## 注意事项

tmm，jackett，sonarr最好配置代理。否则，刮削，图片墙可能工作不正常。

docker最好配置镜像加速，提高安装docker速度

一些docker需要访问github，最好配置代理。

