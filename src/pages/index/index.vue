<template>
  <view class="home-page">
    <view class="content">
      <view class="crumb">
        <view class="crumb-dot"></view>
        <text>首页</text>
      </view>

      <view class="banner-wrap">
        <swiper
          class="banner-swiper"
          :current="currentBanner"
          circular
          autoplay
          :interval="4200"
          :duration="420"
          indicator-dots
          indicator-color="rgba(255, 255, 255, 0.45)"
          indicator-active-color="#ffffff"
          @change="onBannerChange"
        >
          <swiper-item v-for="item in banners" :key="item.title">
            <view class="banner-card" :class="item.theme">
              <view class="banner-copy">
                <text class="banner-kicker">{{ item.kicker }}</text>
                <text class="banner-title">{{ item.title }}</text>
                <text class="banner-desc">{{ item.desc }}</text>
              </view>
              <view class="banner-mark">
                <view class="mark-ring"></view>
                <view class="mark-star">★</view>
                <view class="mark-line mark-line-one"></view>
                <view class="mark-line mark-line-two"></view>
              </view>
            </view>
          </swiper-item>
        </swiper>
        <view class="banner-actions">
          <view class="banner-arrow banner-arrow-left" @tap.stop="slideBanner(-1)">
            <view class="banner-arrow-icon"></view>
          </view>
          <view class="banner-action-line"></view>
          <view class="banner-arrow banner-arrow-right" @tap.stop="slideBanner(1)">
            <view class="banner-arrow-icon"></view>
          </view>
        </view>
      </view>

      <view class="entry-grid">
        <view
          v-for="item in quickLinks"
          :key="item.title"
          class="entry-card"
          hover-class="entry-card-hover"
          @tap="openFeature(item.title)"
        >
          <view class="entry-icon" :class="['entry-icon-' + item.color]">
            <view v-if="item.icon === 'book'" class="icon-book">
              <view class="book-page book-page-left"></view>
              <view class="book-page book-page-right"></view>
            </view>
            <view v-if="item.icon === 'shield'" class="icon-shield">
              <view class="shield-body"></view>
            </view>
            <view v-if="item.icon === 'service'" class="icon-service">
              <view class="service-handle"></view>
              <view class="service-body">
                <view class="service-line"></view>
              </view>
            </view>
            <view v-if="item.icon === 'phone'" class="icon-phone">
              <view class="phone-dot"></view>
            </view>
          </view>
          <text class="entry-title">{{ item.title }}</text>
          <text class="entry-subtitle">{{ item.subtitle }}</text>
        </view>
      </view>

      <view class="notice-card" hover-class="notice-card-hover" @tap="openFeature('近期通知')">
        <view class="notice-icon">
          <view class="notice-shield"></view>
        </view>
        <view class="notice-copy">
          <text class="notice-title">近期通知</text>
          <text class="notice-desc">{{ notice }}</text>
        </view>
        <text class="notice-more">›</text>
      </view>
    </view>

    <view class="tabbar">
      <view v-for="item in tabs" :key="item.title" class="tab-item" :class="{ active: item.active }">
        <view class="tab-icon" :class="['tab-icon-' + item.icon]">
          <view v-if="item.icon === 'home'" class="tab-home-roof"></view>
          <view v-if="item.icon === 'home'" class="tab-home-body"></view>
          <view v-if="item.icon === 'book'" class="tab-book-left"></view>
          <view v-if="item.icon === 'book'" class="tab-book-right"></view>
          <view v-if="item.icon === 'shield'" class="tab-shield-body"></view>
          <view v-if="item.icon === 'user'" class="tab-user-head"></view>
          <view v-if="item.icon === 'user'" class="tab-user-body"></view>
        </view>
        <text>{{ item.title }}</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      currentBanner: 0,
      banners: [
        {
          kicker: '警民协同服务',
          title: '共建平安社区',
          desc: '信息联动、服务下沉，让群众办事更顺畅。',
          theme: 'banner-blue',
        },
        {
          kicker: '普法宣传',
          title: '法治知识随手学',
          desc: '常见案例、政策解读和安全提醒集中查看。',
          theme: 'banner-indigo',
        },
        {
          kicker: '风险防范',
          title: '守好钱袋子',
          desc: '反诈提示及时更新，提高识骗防骗能力。',
          theme: 'banner-cyan',
        },
      ],
      quickLinks: [
        { title: '法治科普中心', subtitle: '政策案例', icon: 'book', color: 'blue' },
        { title: '反诈防护盾', subtitle: '预警提示', icon: 'shield', color: 'orange' },
        { title: '便民服务厅', subtitle: '事项办理', icon: 'service', color: 'green' },
        { title: '互动工具', subtitle: '在线互助', icon: 'phone', color: 'purple' },
      ],
      notice: '本周社区安全宣传活动安排已更新，请居民留意服务大厅公告。',
      tabs: [
        { title: '首页', icon: 'home', active: true },
        { title: '法治科普', icon: 'book', active: false },
        { title: '反诈防护', icon: 'shield', active: false },
        { title: '我的', icon: 'user', active: false },
      ],
    }
  },
  methods: {
    onBannerChange(event) {
      this.currentBanner = event.detail.current
    },
    slideBanner(step) {
      const total = this.banners.length
      this.currentBanner = (this.currentBanner + step + total) % total
    },
    openFeature(name) {
      uni.showToast({
        title: `${name}待接入`,
        icon: 'none',
      })
    },
  },
}
</script>

<style>
page {
  background: #0c5ef5;
}

.home-page {
  min-height: 100vh;
  background: linear-gradient(180deg, #0b62ff 0%, #1d63f0 52%, #f5f7fb 52%, #f5f7fb 100%);
}

.content {
  box-sizing: border-box;
  min-height: 100vh;
  padding: 20rpx 48rpx 168rpx;
}

.crumb {
  display: flex;
  align-items: center;
  gap: 12rpx;
  height: 44rpx;
  font-size: 24rpx;
  color: rgba(255, 255, 255, 0.86);
}

.crumb-dot {
  width: 10rpx;
  height: 10rpx;
  border-radius: 50%;
  background: #68f0b3;
  box-shadow: 0 0 0 6rpx rgba(104, 240, 179, 0.18);
}

.banner-wrap {
  position: relative;
  margin-top: 22rpx;
  padding-bottom: 34rpx;
}

.banner-swiper {
  height: 304rpx;
  border-radius: 64rpx;
  overflow: hidden;
  box-shadow: 0 28rpx 60rpx rgba(6, 36, 102, 0.22);
}

.banner-card {
  position: relative;
  display: flex;
  box-sizing: border-box;
  height: 304rpx;
  padding: 44rpx 54rpx;
  overflow: hidden;
  border: 1rpx solid rgba(255, 255, 255, 0.52);
  border-radius: 64rpx;
}

.banner-blue {
  background: linear-gradient(135deg, #ffffff 0%, #dce9ff 58%, #b6d2ff 100%);
}

.banner-indigo {
  background: linear-gradient(135deg, #ffffff 0%, #e9e7ff 58%, #c9d5ff 100%);
}

.banner-cyan {
  background: linear-gradient(135deg, #ffffff 0%, #dff8ff 58%, #b9e7ff 100%);
}

.banner-copy {
  position: relative;
  z-index: 2;
  width: 430rpx;
}

.banner-kicker {
  display: block;
  margin-bottom: 14rpx;
  font-size: 24rpx;
  color: #1d63f0;
}

.banner-title {
  display: block;
  font-size: 42rpx;
  font-weight: 700;
  line-height: 1.2;
  color: #10233f;
}

.banner-desc {
  display: block;
  margin-top: 18rpx;
  font-size: 24rpx;
  line-height: 1.55;
  color: #51627a;
}

.banner-mark {
  position: absolute;
  right: 34rpx;
  bottom: -44rpx;
  width: 240rpx;
  height: 240rpx;
  opacity: 0.32;
}

.mark-ring {
  position: absolute;
  inset: 0;
  border: 22rpx solid #d79a3c;
  border-radius: 50%;
}

.mark-star {
  position: absolute;
  top: 48rpx;
  left: 78rpx;
  font-size: 70rpx;
  color: #d3473f;
}

.mark-line {
  position: absolute;
  left: 56rpx;
  width: 128rpx;
  height: 18rpx;
  border-radius: 999rpx;
  background: #d3473f;
}

.mark-line-one {
  top: 126rpx;
}

.mark-line-two {
  top: 162rpx;
}

.banner-actions {
  position: absolute;
  right: 28rpx;
  bottom: 0;
  z-index: 3;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8rpx;
  box-sizing: border-box;
  height: 62rpx;
  padding: 8rpx 10rpx;
  border: 1rpx solid rgba(255, 255, 255, 0.76);
  border-radius: 999rpx;
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 16rpx 36rpx rgba(18, 61, 128, 0.18);
}

.banner-arrow {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 46rpx;
  height: 46rpx;
  border-radius: 50%;
  background: transparent;
}

.banner-arrow:active {
  background: rgba(29, 99, 240, 0.1);
}

.banner-action-line {
  width: 1rpx;
  height: 28rpx;
  background: rgba(82, 96, 112, 0.18);
}

.banner-arrow-icon {
  width: 14rpx;
  height: 14rpx;
  border-top: 5rpx solid #2663b8;
  border-right: 5rpx solid #2663b8;
  border-radius: 1rpx;
  box-sizing: border-box;
}

.banner-arrow-left .banner-arrow-icon {
  margin-left: 4rpx;
  transform: rotate(-135deg);
}

.banner-arrow-right .banner-arrow-icon {
  margin-right: 4rpx;
  transform: rotate(45deg);
}

.entry-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 26rpx;
  margin-top: 22rpx;
}

.entry-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
  min-height: 238rpx;
  padding: 32rpx 22rpx;
  border-radius: 30rpx;
  background: #ffffff;
  box-shadow: 0 18rpx 40rpx rgba(8, 43, 103, 0.13);
}

.entry-card-hover {
  transform: translateY(2rpx);
  opacity: 0.92;
}

.entry-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 86rpx;
  height: 76rpx;
  color: #1d63f0;
}

.entry-icon-orange {
  color: #ff7a18;
}

.entry-icon-green {
  color: #35c66b;
}

.entry-icon-purple {
  color: #c83fe0;
}

.entry-title {
  display: block;
  margin-top: 18rpx;
  font-size: 29rpx;
  line-height: 1.35;
  color: #1b2430;
  text-align: center;
}

.entry-subtitle {
  display: block;
  margin-top: 8rpx;
  font-size: 22rpx;
  color: #8b96a8;
}

.icon-book {
  position: relative;
  display: flex;
  width: 78rpx;
  height: 66rpx;
}

.book-page {
  width: 34rpx;
  height: 58rpx;
  border: 7rpx solid currentColor;
  background: #ffffff;
}

.book-page-left {
  border-right-width: 4rpx;
  border-radius: 6rpx 0 0 6rpx;
}

.book-page-right {
  border-left-width: 4rpx;
  border-radius: 0 6rpx 6rpx 0;
}

.icon-shield,
.icon-service,
.icon-phone {
  position: relative;
  width: 78rpx;
  height: 76rpx;
}

.shield-body {
  width: 54rpx;
  height: 62rpx;
  margin: 2rpx auto 0;
  border: 7rpx solid currentColor;
  border-top-left-radius: 12rpx;
  border-top-right-radius: 12rpx;
  border-bottom-left-radius: 28rpx;
  border-bottom-right-radius: 28rpx;
  box-sizing: border-box;
}

.service-handle {
  position: absolute;
  top: 0;
  left: 24rpx;
  width: 30rpx;
  height: 20rpx;
  border: 7rpx solid currentColor;
  border-bottom: 0;
  border-radius: 12rpx 12rpx 0 0;
  box-sizing: border-box;
}

.service-body {
  position: absolute;
  left: 7rpx;
  bottom: 4rpx;
  width: 64rpx;
  height: 58rpx;
  border: 7rpx solid currentColor;
  border-radius: 12rpx;
  box-sizing: border-box;
}

.service-line {
  width: 7rpx;
  height: 44rpx;
  margin: 7rpx auto 0;
  border-radius: 999rpx;
  background: currentColor;
}

.icon-phone {
  width: 52rpx;
  height: 76rpx;
  border: 7rpx solid currentColor;
  border-radius: 12rpx;
  box-sizing: border-box;
}

.phone-dot {
  position: absolute;
  left: 50%;
  bottom: 8rpx;
  width: 7rpx;
  height: 7rpx;
  margin-left: -3.5rpx;
  border-radius: 50%;
  background: currentColor;
}

.notice-card {
  display: flex;
  align-items: center;
  box-sizing: border-box;
  min-height: 100rpx;
  margin-top: 44rpx;
  padding: 18rpx 28rpx;
  border-radius: 16rpx;
  background: linear-gradient(135deg, #ff8a25 0%, #ffb13b 100%);
  box-shadow: 0 18rpx 38rpx rgba(178, 87, 16, 0.22);
}

.notice-card-hover {
  opacity: 0.9;
}

.notice-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 60rpx;
  height: 60rpx;
  margin-right: 20rpx;
  color: #ffffff;
}

.notice-shield {
  width: 42rpx;
  height: 48rpx;
  border: 7rpx solid currentColor;
  border-top-left-radius: 10rpx;
  border-top-right-radius: 10rpx;
  border-bottom-left-radius: 22rpx;
  border-bottom-right-radius: 22rpx;
  box-sizing: border-box;
}

.notice-copy {
  flex: 1;
  min-width: 0;
}

.notice-title {
  display: block;
  font-size: 32rpx;
  font-weight: 700;
  color: #ffffff;
}

.notice-desc {
  display: block;
  margin-top: 6rpx;
  overflow: hidden;
  font-size: 23rpx;
  color: rgba(255, 255, 255, 0.88);
  text-overflow: ellipsis;
  white-space: nowrap;
}

.notice-more {
  margin-left: 18rpx;
  font-size: 50rpx;
  color: #ffffff;
}

.tabbar {
  position: fixed;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 9;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  height: 118rpx;
  padding-bottom: env(safe-area-inset-bottom);
  border-top: 1rpx solid rgba(14, 28, 52, 0.08);
  background: rgba(255, 255, 255, 0.98);
}

.tab-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 8rpx;
  color: #101820;
  font-size: 24rpx;
}

.tab-item.active {
  color: #0b62ff;
  font-weight: 600;
}

.tab-icon {
  position: relative;
  width: 52rpx;
  height: 52rpx;
  color: currentColor;
}

.tab-home-roof {
  position: absolute;
  top: 2rpx;
  left: 9rpx;
  width: 30rpx;
  height: 30rpx;
  border-top: 7rpx solid currentColor;
  border-left: 7rpx solid currentColor;
  transform: rotate(45deg);
  box-sizing: border-box;
}

.tab-home-body {
  position: absolute;
  right: 7rpx;
  bottom: 3rpx;
  left: 7rpx;
  height: 28rpx;
  border: 7rpx solid currentColor;
  border-top: 0;
  border-radius: 4rpx;
  box-sizing: border-box;
}

.tab-book-left,
.tab-book-right {
  position: absolute;
  top: 7rpx;
  width: 22rpx;
  height: 34rpx;
  border: 6rpx solid currentColor;
  box-sizing: border-box;
}

.tab-book-left {
  left: 3rpx;
  border-right-width: 3rpx;
  border-radius: 5rpx 0 0 5rpx;
}

.tab-book-right {
  right: 3rpx;
  border-left-width: 3rpx;
  border-radius: 0 5rpx 5rpx 0;
}

.tab-shield-body {
  width: 38rpx;
  height: 44rpx;
  margin: 3rpx auto 0;
  border: 6rpx solid currentColor;
  border-top-left-radius: 9rpx;
  border-top-right-radius: 9rpx;
  border-bottom-left-radius: 20rpx;
  border-bottom-right-radius: 20rpx;
  box-sizing: border-box;
}

.tab-user-head {
  width: 22rpx;
  height: 22rpx;
  margin: 2rpx auto 0;
  border: 6rpx solid currentColor;
  border-radius: 50%;
  box-sizing: border-box;
}

.tab-user-body {
  width: 42rpx;
  height: 24rpx;
  margin: 3rpx auto 0;
  border: 6rpx solid currentColor;
  border-bottom: 0;
  border-radius: 24rpx 24rpx 0 0;
  box-sizing: border-box;
}
</style>
