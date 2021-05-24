<template>
    <view class="container">
        <view class="left-top-sign">LOGIN</view>
        <view class="welcome">源升建材，欢迎您！</view>
        <view v-if="!boolShowform">
            <button class="confirm-btn" open-type="getUserInfo" :disabled="logining" @getuserinfo="wxLogin">微信授权登录</button>
            <view class="padding flex flex-direction btn-view">
                <button class="cu-btn bg-orange margin-tb-sm lg" @click="cancelLogin">取消</button>
            </view>
        </view>
        <form v-if="boolShowform">
            <view class="cu-form-group">
                <view class="title">姓名</view>
                <input v-model="form.nane" placeholder="请输入真实姓名" name="input" />
            </view>
            <view class="cu-form-group">
                <view class="title">收货地址</view>
                <input v-model="form.address" placeholder="请输入收货地址" name="input" />
                <text class="cuIcon-locationfill text-orange" />
            </view>
            <view class="cu-form-group">
                <view class="title">手机号码</view>
                <input v-model="form.PhoneNum" placeholder="请输入收货人手机号码" name="input" />
            </view>
            <view class="padding flex flex-direction btn-view">
                <button class="cu-btn bg-red margin-tb-sm lg" @click="login">登录</button>
            </view>
        </form>
    </view>
</template>
<script>
export default {
    data() {
        return {
            boolShowform: false,
            form: {}
        }
    },
    methods: {
        wxLogin(e) {
            const that = this
            that.logining = true
            const userInfo = e.detail.userInfo
            console.log(userInfo, e)
            // eslint-disable-next-line no-undef
            uni.login({
                provider: 'weixin',
                success: async login_res => {
                    const code = login_res.code
                    console.log(login_res, code)
                    // 如果code存在，获取appid
                    if (code) {
                        await new Promise((resolve, reject) => {
                            uni.getUserInfo({
                                success(info_res) {
                                    console.log(info_res)
                                    that.boolShowform = true
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
                                    resolve()
                                }
                            })
                        })
                    } else {
                        uni.showToast({
                            title: '授权失败，请重新授权！',
                            duration: 2000,
                            icon: 'none'
                        })
                    }
                }
            })
        },
        // 登录
        login() {
            console.log(this.form)
        },
        // 取消登录
        cancelLogin() {
            // eslint-disable-next-line no-undef
            uni.switchTab({
                url: '/pages/index/index'
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
        margin-top: -300upx;
    }
    .welcome {
        position: relative;
        left: 50upx;
        font-size: 46upx;
        color: #555;
        text-shadow: 1px 0px 1px rgba(0, 0, 0, 0.3);
    }
    .confirm-btn {
        width: calc(100% -20px);
        margin: 0 10px;
        height: 76upx;
        line-height: 76upx;
        border-radius: 5px;
        margin-top: 70upx;
        background: $uni-color-primary;
        color: #fff;
        font-size: $font-lg;
    }
}
form{
    border-top: 1rpx solid #eee;
    margin-top: 20px;
}
.btn-view{
    border-top: 1rpx solid #eee;
    .bg-red{
        background-color: $uni-color-primary;
    }
}
.cu-form-group .title {
    min-width: calc(4em + 15px);
}
</style>
<style lang="scss">
page{
    height: 100%;
}
</style>
