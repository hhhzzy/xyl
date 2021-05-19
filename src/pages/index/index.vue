<template>
	<view class="mine-box">
        <swiper class="screen-swiper" :class="dotStyle?'square-dot':'round-dot'" :indicator-dots="true" :circular="true"
		 :autoplay="true" interval="5000" duration="500">
			<swiper-item v-for="(item,index) in swiperList" :key="index">
				<image :src="item.url" mode="aspectFill" v-if="item.type=='image'"></image>
				<video :src="item.url" autoplay loop muted :show-play-btn="false" :controls="false" objectFit="cover" v-if="item.type=='video'"></video>
			</swiper-item>
		</swiper>
        <view class="scroll-box">
            <scroll-view class="scroll-view_H" scroll-x="true" @scroll="scroll" scroll-left="120">
                <view id="demo1" class="scroll-view-item_H uni-bg-red">
                    
                </view>
                <view id="demo2" class="scroll-view-item_H uni-bg-green" style="background-color:blue;">B</view>
                <view id="demo3" class="scroll-view-item_H uni-bg-blue">C</view>
            </scroll-view>
        </view>
    </view>
</template>

<script>
	export default {
		data() {
			return {
				swiperList: [{
					id: 0,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big84000.jpg'
				}, {
					id: 1,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big37006.jpg',
				}, {
					id: 2,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big39000.jpg'
				}, {
					id: 3,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big10001.jpg'
				}, {
					id: 4,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big25011.jpg'
				}, {
					id: 5,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big21016.jpg'
				}, {
					id: 6,
					type: 'image',
					url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big99008.jpg'
				}],
                scrollTop: 0,
                old: {
                    scrollTop: 0
                }
			};
		},
        onLoad() {
			// 初始化towerSwiper 传已有的数组名即可
		},
        onShow(){
        },
        methods:{
            scroll: function(e) {
                console.log(e)
                this.old.scrollTop = e.detail.scrollTop
            }
        }
	}

</script>

<style>
	.scroll-Y {
		height: 300px;
	}
	.scroll-view_H {
		white-space: nowrap;
		width: 100%;
        background-color: red;
	}
	.scroll-view-item {
		height: 100px;
		line-height: 100px;
		text-align: center;
		font-size: 36px;
	}
	.scroll-view-item_H {
		display: inline-block;
		width: 100%;
		height: 100px;
		line-height: 100px;
		text-align: center;
		font-size: 36px;
	}
    .scroll-box{
        margin-top: 20rpx;
    }
</style>
