<template>
    <view class="container">
        <view class="left-top-sign">LOGIN</view>
        <view class="welcome">欢迎回来！</view>
        <button class="confirm-btn" open-type="getUserInfo" :disabled="logining" @getuserinfo="wxLogin">微信授权登录</button>
    </view>
</template>
<script>
export default {
    data() {
        return {

        }
    },
    methods: {
        wxLogin(e) {
            const that = this
            that.logining = true
            const userInfo = e.detail.userInfo
            console.log(e)
            // eslint-disable-next-line no-undef
            uni.login({
                provider: 'weixin',
                success: login_res => {
                    const code = login_res.code
                    console.log(login_res)
                    // eslint-disable-next-line no-undef
                    uni.getUserInfo({
                        success(info_res) {
                            console.log(info_res)
                            // eslint-disable-next-line no-undef
                            // uni.request({
                            //     url: 'http://localhost:8080/wxlogin',
                            //     method: 'POST',
                            //     header: {
                            //         'content-type': 'application/x-www-form-urlencoded'
                            //     },
                            //     data: {
                            //         code: code,
                            //         rawData: info_res.rawData
                            //     },
                            //     success(res) {
                            //         if (res.data.status == 200) {
                            //             that.$store.commit('login', userInfo)
                            //         // uni.setStorageSync("userInfo",userInfo);
                            //         // uni.setStorageSync("skey", res.data.data);
                            //         } else {
                            //             console.log('服务器异常')
                            //         }
                            //     },
                            //     fail(error) {
                            //         console.log(error)
                            //     }
                            // })
                            // eslint-disable-next-line no-undef
                            uni.hideLoading()
                            // eslint-disable-next-line no-undef
                            uni.navigateBack()
                        }
                    })
                }
            })
        }
    }
}
</script>
<style lang="scss" scoped>

.container {
    display: flex;
    overflow: hidden;
    background: #fff;
    flex-direction: column;
    justify-content: center;
    height: 100%;
    .left-top-sign {
        font-size: 120upx;
        color: $page-color-base;
        position: relative;
        left: -10upx;
        margin-top: -100upx;
    }
    .welcome {
        position: relative;
        left: 50upx;
        top: -90upx;
        font-size: 46upx;
        color: #555;
        text-shadow: 1px 0px 1px rgba(0, 0, 0, 0.3);
    }
    .confirm-btn {
        width: 630upx;
        height: 76upx;
        line-height: 76upx;
        border-radius: 50px;
        margin-top: 70upx;
        background: $uni-color-primary;
        color: #fff;
        font-size: $font-lg;
        &:after {
            border-radius: 100px;
        }
    }
}
</style>
<style lang="scss">
page{
    height: 100%;
}
</style>
