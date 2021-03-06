## wechat-calendar-plugin

<img width="300" align="center" src="picture.jpg"/>

## paramters

属性  | 描述 | 类型 | 默认值
---- | ---- | -- | ------
dates | 优先级相对其他pro最高，主要用于再次打开恢复状态使用。| Array  | []
startTime | 可选起始日期时间。通过js的api设置的时间优先级低于pro。    | String  | 今日  
defaultDays | 默认可选日期数    | Number  | 100
endTime | 可选结束日期时间    | String  | 加上defaultDays后得到的日期，默认100。如果同时设置defaultDays和endTime，以小者为准。通过js的api  设置的时间优先级低于pro。
activeDateIndex | 默认高亮激活指定索引的日期    | Number  | 0
scrollToDateIndex | 日期滑动条滚动到指定索引的日期    | Number  | 0
defaultCoverStartHourIndex | 首个激活打开的日期，默认选择的时间起始值    | Number  | 3
defaultCoverEndHourIndex | 首个激活打开的日期，默认选择的时间结束值    | Number  | 6
startHour | 每日的起始时间| Number  | 0
endHour | 每日的结束时间| Number  | 24
useSwiper | 是否启用swiper控件，用于滚动时间选择器的横向滑动。当备选日期比较多时容易影响使用体验，请注意。  | Boolean    | false  

## snippets

### page.wxml

```html
<date-time-picker
	binddoneevent="onDoneEvent"
	dates="{{dates}}"
	start-time=""
	default-days="300"
	active-date-index="{{activeDateIndex}}"
	default-cover-start-hour-index='3'
	default-cover-end-hour-index='6'
	start-hour='6'
	end-hour=''
	use-swiper="{{false}}" />
```

### page.json

```json
{
	"navigationBarBackgroundColor": "#051631",
	"navigationBarTextStyle": "white",
	"navigationBarTitleText": "Time Picker",
	"usingComponents": {
		"date-time-picker": "plugin://myPlugin/date-time-picker"
	}
}
```

### page.js

```js
var plugin = requirePlugin("myPlugin");
let app = getApp();
Page({
	data: {
		dates: [],
		activeDateIndex: 0,
	},
	onLoad: function(options) {
		this.setData({
			dates: app.globalData.dates || [],
			activeDateIndex: app.globalData.activeDateIndex || 0
		});
	},
	onDoneEvent: function(e) {
		console.log(e);
		app.globalData.totalTime = e.detail.totalTime;
		app.globalData.dates = e.detail.dates;
		app.globalData.activeDateIndex = e.detail.activeDateIndex;
		wx.navigateBack();
	}
})
```

### app.json

```json
{
	"pages": [],
	"plugins": {
		"myPlugin": {
			"version": "1.0.1",
			"provider": "wxbdba0f18d2aa9aa1"
		}
	}
}
```

### app.js

```js
App({
	onLaunch: function() {},
	globalData: {
		totalTime: undefined
	}
})
```
