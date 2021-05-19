<template>
    <view class="mine-box">
        <swiper
            class="screen-swiper"
            :class="dotStyle?'square-dot':'round-dot'"
            :indicator-dots="true"
            :circular="true"
            :autoplay="true"
            interval="5000"
            duration="500"
        >
            <swiper-item v-for="(item,index) in swiperList" :key="index">
                <image v-if="item.type=='image'" :src="item.url" mode="aspectFill" />
                <video v-if="item.type=='video'" :src="item.url" autoplay loop muted :show-play-btn="false" :controls="false" objectFit="cover"></video>
            </swiper-item>
        </swiper>
        <view class="tab-box">
            <view class="cu-list grid col-4 no-border">
                <view class="cu-item">
                    <view class="text-red">
                        <img src="" alt="" />
                    </view>
                    <text>vr</text>
                </view>
                <view class="cu-item">
                    <view class="cuIcon-cardboardfill text-red">
                        <view class="cu-tag " />
                    </view>
                    <text>vr</text>
                </view>
                <view class="cu-item">
                    <view class="cuIcon-cardboardfill text-red">
                        <view class="cu-tag " />
                    </view>
                    <text>vr</text>
                </view>
                <view class="cu-item">
                    <view class="cuIcon-cardboardfill text-red">
                        <view class="cu-tag " />
                    </view>
                    <text>vr</text>
                </view>
            </view>
        </view>
        <view class="goods-box">
            <view class="title">油漆系列</view>
            <view class="cu-list grid col-4 no-border">
                <view class="cu-item">
                    <view class="text-red">
                        <img src="https://ossweb-img.qq.com/images/lol/web201310/skin/big84000.jpg" alt="" />
                    </view>
                    <text>vr</text>
                </view>
                <view class="cu-item">
                    <view class="cuIcon-cardboardfill text-red">
                        <view class="cu-tag " />
                    </view>
                    <text>vr</text>
                </view>
                <view class="cu-item">
                    <view class="cuIcon-cardboardfill text-red">
                        <view class="cu-tag " />
                    </view>
                    <text>vr</text>
                </view>
                <view class="cu-item">
                    <view class="cuIcon-cardboardfill text-red">
                        <view class="cu-tag " />
                    </view>
                    <text>vr</text>
                </view>
            </view>
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
                url: 'https://ossweb-img.qq.com/images/lol/web201310/skin/big37006.jpg'
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
        }
    },
    onLoad() {
        // 初始化towerSwiper 传已有的数组名即可
    },
    onShow() {
    },
    methods: {
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
    .tab-box{
        margin-top: 10px;
        padding: 10px;
        background-color: #fff;
    }
    .tab-box img{
        height: 100%;
    }
    .goods-box{
        background-color: #fff;
        margin-top: 10px;
    }
    .goods-box .title{
        font-size: 20px;
        font-weight: bold;
        color: #666;
        padding: 10px;
    }
    .goods-box img{
        height: 100%;
    }
</style>
