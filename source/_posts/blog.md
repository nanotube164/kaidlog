---
title: 如何在部落格加入你的旅行足跡 How to add your footprint in your blog
date: 2019-11-23 19:57:15
tags: footprint
categories: 
 - Software Development
 - Blog

top_img: https://i.imgur.com/GxNu6t4.jpg
cover: https://i.imgur.com/GxNu6t4.jpg
---

# How to use jVectorMap to create your own traveling footprint

![My footprint](https://i.imgur.com/TqaKqox.png)

## jVectorMap

JVectorMap 是一個優秀的、兼容性強的 jQuery 地圖插件。

它可以工作在包括 IE6 在内的各款瀏覽器中，矢量圖輸出，除官方提供各國地圖資料外，用戶可以使用數據轉換程序定制地圖數據。例如街道地圖、小區地圖等等。

![jVectorMap](http://wx4.sinaimg.cn/large/cf5b72a1ly1fvv2t7olhjj20ss0e8jvo.jpg)

那麼今天的目標就是打造自己的足跡地圖並放置到自己的 Blog 上

## 目錄結構

![](https://i.imgur.com/9kRBcwL.png)

- 红色框中的文件是必须要引入的内容。

- 藍色框中的文件是展示的地圖，可自行到官網下載需要的地圖 : <http://jvectormap.com/maps/world/world/>，複製到 js 目錄。

- index.html 中需要添加足跡位置和相關樣式。

## 開始

 `index.html` 分為三部分介紹：
 
 - 如何更換不同國家地圖。
 
 
 - 如何修改地圖顏色等相關樣式。
 
 
 - 如何添加足跡位置。
 
## 第一部分：如何更換不同國家地圖。
 
```html
<html>
	<head>
		<!--import jQuery framework-->
		<script type="text/javascript" src="js/jquery-1.9.1.min.js"></script>
		<!--加入jVectorMap-->
		<script type="text/javascript" src="js/jquery-jvectormap-1.2.2.min.js"></script>
		<!--import css-->
		<link href="js/jquery-jvectormap-1.2.2.css" rel="stylesheet" media="screen">


		<!--import chinese map database-->
		<!--script type="text/javascript" src="js/jquery-jvectormap-cn-merc-en.js"></script-->

		<!--import US map database-->
		<!--script type="text/javascript" src="js/jquery-jvectormap-us-aea.js"></script-->
		<!--import world map database-->
		<script type="text/javascript" src="js/jquery-jvectormap-world-mill.js"></script>

	</head>
<body>
```
提前下載需要的國家地圖，複製到 js 目錄下。

在 `<head>` 標籤裡引入地圖資料： `<script type="text/javascript" src="js/地圖文件名"></script>`

**注意** ：同時只能有一個地圖庫，注意不要引入多個地圖數據。可以選擇注釋掉其他的，方便更改。

## 第二部分：如何修改地圖顏色等相關樣式。


```html
	<!--background-color: 地圖背景颜色-->
	<div id="map" style="background-color:#353535"> </div>
	<script>
		$('#map').vectorMap({

			// 此處更改地圖
			//map: 'cn_merc_en',   // 中國地圖
			//map: 'us-aea',     // 美國地圖
			map: 'world-mill', // 世界地圖


			backgroundColor: 'transparent',
			zoomMin: 0.9, // 鼠標縮放時的最小比例
			zoomMax: 2.4, // 鼠標縮放時的最大比例
			focusOn: {
				x: 0.55,
				y: 2,
				scale: 0.9
			},
			regionStyle: {
				initial: {
					fill: '#e5e5e5',   // 地圖顏色
					"fill-opacity": 1, // 省份（州）是否隱藏，鼠標滑動時顯示; 1：顯示，2：隱藏。
					stroke: 'none',
					"stroke-width": 0,
					"stroke-opacity": 1
				},
				hover: {
					fill: '#ccc',  // 鼠標滑動至某省分的高亮顏色。
					"fill-opacity": 0.8
				},
				selected: {
					fill: 'yellow'
				},
				selectedHover: {}
			},
			markerStyle: {
		        initial: {
		            fill: '#fd8888', // 足跡位置的填充顏色
		            stroke: '#fff'   // 足跡位置的描邊顏色
		        },
				hover: {
					fill: '#fd2020', // 鼠標滑動至足跡位置後的填充顏色
					stroke: '#fff',  // 鼠標滑動至足跡位置後的描邊顏色
					"fill-opacity": 0.8
				},
		    },
		});
	</script>
</html>

```
參照代碼注釋修改顏色和相關樣式。

**千萬注意** ：在更改地图时 `map: '地圖名稱'`  ，地圖名稱是地圖數據文件名的後半部分。

例如：

美國地圖文件名：jquery-jvectormap-us-aea.js

那地圖的名稱是：us-aea

**但是要注意把 `-` (横槓)更改成 `_`（下滑線）。 否則不會顯示地圖。**

## 第三部分：如何添加足跡位置。

```html
	markers: [ // 足跡位置

		// {latLng: [經度（保留兩位小數）, 緯度（保留兩位小數）], name: '城市名稱'},
		// 推荐查詢經緯度網站：http://www.gpsspg.com/maps.htm

		{latLng: [37.53,-122.19], name: 'LA'},
		{latLng: [35.97,-114.92], name: 'LV'},
		{latLng: [25.03,121.52], name: 'Taipei'},
		{latLng: [22.99,120.18], name: 'Tainan'},
	]

```

推薦查經緯度網站：http://www.gpsspg.com/maps.htm

語法：`{latLng: [經度（保留兩位小數）, 緯度（保留兩位小數）], name: '城市名稱'},`。

## 如何嵌入式到Blog中

```html
<iframe style="max-width: 100%" 
      frameborder="no" 
      border="0" 
      marginwidth="0" 
      marginheight="0" 
      width="100%" 
      height="750px" 
      src="替換成你的足跡地圖連結">                                        
</iframe>

```
把製作好的足跡地圖文件放在 server 上，把訪問連結放在 `src` 中。

然後將上面的 code 複製到你的 Blog 頁面上即可。

可配合手機端和等比例縮放。

## 下載代碼

```
git clone https://github.com/daekony/traveling-footprint-creater
```







