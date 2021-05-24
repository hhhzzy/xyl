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
        <view v-for="(item,index) in typeArr" :key="index" class="goods-box">
            <view class="title">{{ item.typeName }}</view>
            <scroll-view class="scroll-view_H" scroll-x="true" @scroll="scroll">
                <view v-if="item.goods && item.goods.length">
                    <view v-for="(ele,ind) in item.goods" :key="ind" class="scroll-view-item_H goods-list">
                        <img :src="url+ele.GoodsImgs" alt="" />
                        <text class="name">{{ ele.GoodsName }}</text>
                        <text class="text-price text-red">{{ ele.ShopPrice }}</text>
                    </view>
                </view>
                <view v-else class="view-no-text">
                    暂无商品！
                </view>
            </scroll-view>
        </view>

    </view>
</template>

<script>
import ajax from '@/utils/http.js'
import { url } from '@/utils/url.js'
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
            },
            typeArr: [

            ],
            url: url
        }
    },
    async onLoad() {
        // 初始化towerSwiper 传已有的数组名即可

        await this.getGoodsTypeList()
        this.getGoods()
        console.log(555)
    },
    onShow() {
    },
    methods: {
        scroll: function(e) {
            console.log(e)
            this.old.scrollTop = e.detail.scrollTop
        },
        // 获取商品类别
        getGoodsTypeList() {
            return new Promise((resolve, reject) => {
                ajax.get('/Mall/InquireGoodType?typeLevel=1&showIndex=1').then(res => {
                    if (res.data.code === 200) {
                        res.data.result.forEach(item => {
                            this.typeArr.push({
                                typeName: item.CategoryName,
                                typeId: item.CategoryId
                            })
                        })
                    }
                    resolve()
                    console.log(this.typeArr)
                })
            })
        },
        // 获取商品列表
        getGoods() {
            if (this.typeArr && this.typeArr.length) {
                this.typeArr.forEach((item, index) => {
                    console.log(item.typeId)
                    ajax.get('/Mall/getGoodsList?pageIndex=1&pageSize=1000&showIndex=1&typeId=' + item.typeId + '&typeLevel=1').then(res => {
                        this.$set(this.typeArr[index], 'goods', res.data.result.goodsList)
                        console.log(this.typeArr)
                    })
                })
            }
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
    .goods-box:last-child{
        margin-bottom: 10px;
    }
    .goods-box .title{
        font-size: 20px;
        font-weight: bold;
        color: #666;
        padding: 10px;
    }
    .goods-box img{
        width: 78px;
        height: 75px;
        display: block;
    }
    .goods-box .name{
        height: 18px;
        line-height: 18px;
        overflow: hidden;
        font-size: 14px;
        display: block;
    }
    .goods-box .text-price{
        display: block;
        font-size: 16px;
        line-height: 20px;
    }
    .goods-box .goods-list{
        width: 100px;
        padding: 10px;
        height: 130px;
    }
    .view-no-text{
        text-align: center;
        margin: 15px 0;
        height: 50px;
    }
</style>
