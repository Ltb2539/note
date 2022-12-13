## 样式

### 字体

首行缩进2字符

```css
text-indent: 2em;
```

### Position(定位)

#### static 定位

HTML 元素的默认值，即没有定位，遵循正常的文档流对象。

静态定位的元素不会受到 top, bottom, left, right影响。

```css
div.static {
    position: static;
    border: 3px solid #73AD21;
}
```

#### fixed 定位

元素的位置相对于浏览器窗口是固定位置。

即使窗口是滚动的它也不会移动：



#### relative 定位

相对定位元素的定位是相对其正常位置。

#### absolute 定位

绝对定位的元素的位置相对于最近的已定位父元素，如果元素没有已定位的父元素，那么它的位置相对于<html>:

#### sticky 定位

sticky 英文字面意思是粘，粘贴，所以可以把它称之为粘性定位。

**position: sticky;** 基于用户的滚动位置来定位。

粘性定位的元素是依赖于用户的滚动，在 **position:relative** 与 **position:fixed** 定位之间切换。

它的行为就像 **position:relative;** 而当页面滚动超出目标区域时，它的表现就像 **position:fixed;**，它会固定在目标位置。

元素定位表现为在跨越特定阈值前为相对定位，之后为固定定位。

这个特定阈值指的是 top, right, bottom 或 left 之一，换言之，指定 top, right, bottom 或 left 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。

**注意:** Internet Explorer, Edge 15 及更早 IE 版本不支持 sticky 定位。 Safari 需要使用 -webkit- prefix (查看以下实例)。

### letter-spacing:（字距）

```css
letter-spacing: -3;
```



## 背景图

```vue
<template>
	<view style="width: 100%;height: 100%;">
		<view class="header-content">
			<image src="图片路径" style="width:100%;height:260rpx;"></image>
		</view>

	</view>
</template>
```



```css
	
.header-content {
		position: absolute;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		width: 100%;
		z-index: -1;
		overflow: hidden;
		box-sizing: border-box;
	}
```

## 自定义列表

```vue
<view style="margin-bottom: 200rpx;">
				<!-- 标题 -->
				<view style="font-size: 30rpx;font-weight: bold;margin-bottom: 20rpx;">患者档案</view>
				<!-- 列表 -->
				<view class="hzda_list" v-for="(ditem,index) in dalist" @click="clickda" :key='index' :data-index="index">
					<!-- 头像 -->
					<view class="flex align-center justify-start " style="width: 18%;">
						<image :src="ditem.img" style="height: 72rpx;width: 72rpx;border-radius: 50%;"></image>
					</view>
					<!-- 信息 -->
					<view style="width: 70%">
						<view style="font-size: 30rpx;color: #333333;font-weight: bold;">{{ditem.name}}</view>
						<view style="color: #999999;font-size: 26rpx;">
							<text style="margin-right: 20rpx;" v-if="ditem.sex == 0">未知</text>
							<text style="margin-right: 20rpx;" v-else-if="ditem.sex == 1">男</text>
							<text style="margin-right: 20rpx;" v-else>女</text>
							<text>{{ditem.age}}</text>
						</view>
					</view>
					<!-- 箭头 -->
					<view class="flex align-center justify-end" style="width: 10%;">
						<u-icon name="arrow-right" color="#C0C0C0"></u-icon>
					</view>
				</view>
			</view>
```

```css
.hzda_list {
		background-color: #FFFFFF;
		display: flex;
		border-radius: 10rpx;
		padding: 30rpx;
		margin-bottom: 20rpx;
		box-shadow: 0px 2px 12px 0px rgba(0, 0, 0, 0.04);
	}
```

![image-20201027142458266](C:\Users\25396\AppData\Roaming\Typora\typora-user-images\image-20201027142458266.png)

## 紧贴底部的按钮

```vue
<view class="bottomButton">
			<view class="b">
				<u-button shape="circle" :custom-style="bStyle" >电话随访</u-button>
			</view>
			<view class="b">
				<u-button shape="circle" :custom-style="btStyle" v-if="!guanzhu" @click="gzclick">关注</u-button>
				<u-button shape="circle" :custom-style="bfStyle" v-else @click="gzclick">已关注</u-button>
			</view>
		</view>
```

```css
.bottomButton {
		position: fixed;
		bottom: 0;
		left: 0;
		width: 100%;
		height: 100rpx;
		display: flex;
		align-items: center;
		justify-content: flex-end;
		background-color: #FFFFFF;
		z-index: 1;	
	.b {	/*按钮样式*/
		margin-right: 30rpx;
		padding: 20rpx 0rpx;
		height: 100%;
		width: 150rpx;
	}
}
```
![image-20201027152125554](C:\Users\25396\AppData\Roaming\Typora\typora-user-images\image-20201027152125554.png)

## 不浮动的列表

```vue
<view style="padding: 36rpx 28rpx;" class="flex align-center justify-around">
	<view style="width: 95%;font-size: 28rpx;background-color: ;">修改密码</view>
	<view class="flex align-center">
		<u-icon name="arrow-right" color="#C0C0C0"></u-icon>
	</view>
</view>
```

![image-20201029203101561](C:\Users\25396\AppData\Roaming\Typora\typora-user-images\image-20201029203101561.png)