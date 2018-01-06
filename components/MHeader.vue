<template>
  <section class="header-wrapper2">
    <section class="header-wrapper">
      <div class="header-wrapper-right"></div>
      <header class="header">
        <!--左侧-->
        <div
          class="left c-gap-left-large c-btn"
          @click="handleHeaderLeftClick">
          <div class="logo">
            logo
          </div>
          <div class="left-right c-gap-left">
            <div class="row1">百家车</div>
            <div class="row2 c-gap-top-small">slogan</div>
          </div>
        </div>
        <!--右侧-->
        <nav class="nav">
          <!--导航按钮-->
          <div
            class="nav-item"
            v-for="(item, index) in navList"
            :key="index"
            @mouseenter="handleMouseEnter(index)"
            @mouseleave="handleMouseLeave(index)">
            {{item.text}}
            <transition name="fade">
              <div
                class="mask"
                v-show="item.isShowMask">
                <div
                  v-for="(item2, index2) in item.children"
                  :key="index2"
                  class="mask-item c-gap-inner-left-large transition-animate"
                  @click="handleMaskItemClick(item2)">
                  {{item2.text}}
                </div>
              </div>
            </transition>
          </div>
          <!--登录注册-->
          <div
            v-if="!isLogin"
            class="login">
            <i class="iconfont icon-round-user-new"></i>
            <div class="text c-gap-top-small">
              <span
                class="sign-in transition-animate c-btn"
                @click="handleSignInClick">
                登录
              </span>/<span
              class="sign-up transition-animate c-btn"
              @click="handleSignUpClick">
                注册
              </span>
            </div>
          </div>
          <!--已登录-->
          <div
            v-if="isLogin"
            class="login c-btn"
            @mouseenter="handleLoginMouseEnter()"
            @mouseleave="handleLoginMouseLeave()">
            <div
              class="avatar"
              :style="{
                'background-image': 'url(' + userInfo.avatar + ')'
              }">
            </div>
            <div class="text c-gap-top-small">
              下午好，赵女士
            </div>
            <!--浮层-->
            <transition name="fade">
              <div
                class="mask"
                v-show="userInfo.isShowMask">
                <div
                  v-for="(item, index) in userInfo.children"
                  :key="index"
                  class="mask-item c-gap-inner-left-large transition-animate"
                  @click="handleLoginMaskClick(item, index)">
                  {{item.text}}
                </div>
              </div>
            </transition>
          </div>
        </nav>
        <!--金融计算器模态框-->
        <financial-calculator-modal
          v-if="isShowFinancialCalculatorModal"
          class="financial-calculator"
          @close="handleFinancialCalculatorModalClose">
        </financial-calculator-modal>
        <!--登录注册模态框-->
        <login-modal
          v-if="isShowLoginModal"
          @close="handleLoginModalClose">
        </login-modal>
      </header>
    </section>
  </section>
</template>

<script>
  import FinancialCalculatorModal from './FinancialCalculatorModal.vue';
  import LoginModal from './LoginModal.vue';

  export default {
    name: 'Header',
    data() {
      return {
        isLogin: true,
        isShowFinancialCalculatorModal: false,
        isShowLoginModal: false,
        navList: [
          {
            text: '地区选择',
            isShowMask: false,
            children: [
              {
                text: '自动定位'
              },
              {
                text: '手动输入'
              }
            ]
          },
          {
            text: '买车',
            isShowMask: false,
            children: [
              {
                text: '按品牌',
                link: '/filter'
              },
              {
                text: '按车型',
                link: '/filter'
              }
            ]
          },
          {
            text: '卖车',
            isShowMask: false,
            children: [
              {
                text: '私人卖家'
              },
              {
                text: '经销商'
              }
            ]
          },
          {
            text: '金融',
            isShowMask: false,
            children: [
              {
                text: '金融计算器'
              },
              {
                text: '贷款申请',
                link: '/loanapplication'
              },
              {
                text: '经销商'
              }
            ]
          },
          {
            text: '物流',
            isShowMask: false,
            children: [
              {
                text: '拖车服务'
              }
            ]
          }
        ],
        userInfo: {
          avatar: 'http://img.hb.aicdn.com/d1e4b888292b51aabc1d773d567f8a11fe1411c31428d1-c0wvIo_fw658',
          isShowMask: false,
          children: [
            {
              text: '寻车笔记',
              link: '/personinfo'
            },
            {
              text: '发布卖车',
              link: '/publishcarinfo'
            },
            {
              text: '物流订单',
              link: '/logisticsorder'
            }
          ]
        }
      }
    },
    methods: {
      handleMouseEnter(index) {
        this.navList[index].isShowMask = true;
      },
      handleMouseLeave(index) {
        this.navList[index].isShowMask = false;
      },
      handleLoginMouseEnter() {
        this.userInfo.isShowMask = true;
      },
      handleLoginMouseLeave() {
        this.userInfo.isShowMask = false;
      },
      handleSignInClick() {
        console.log('点击登录');
        this.isShowLoginModal = true;
      },
      handleSignUpClick() {
        console.log('点击注册');
        this.isShowLoginModal = true;
      },
      handleHeaderLeftClick() {
        this.$router.push('/index');
      },
      // 蒙层项点击事件
      handleMaskItemClick(item) {
        if (item.text === '金融计算器') {
          this.isShowFinancialCalculatorModal = true;
          return;
        }
        if (item.link) {
          this.$router.push(item.link);
        }
      },
      // 登录项蒙层点击事件
      handleLoginMaskClick(item, index) {
        console.log('item', item, index);
        if (item.link) {
          this.$router.push(item.link);
        }
      },
      // 关闭金融计算器
      handleFinancialCalculatorModalClose() {
        console.log('handleFinancialCalculatorModalClose');
        this.isShowFinancialCalculatorModal = false;
      },
      // 登录模态框关闭事件
      handleLoginModalClose() {
        this.isShowLoginModal = false;
      }
    },
    components: {
      FinancialCalculatorModal,
      LoginModal
    }
  }
</script>

<style lang="scss" scoped>
  @import "../assets/app.scss";

  .header-wrapper2 {
    position: fixed;
    width: 100%;
    box-shadow: 0 0 5px 1px $primaryColor;
    background: #fff;
    z-index: 8;
  }

  .header-wrapper {
    position: relative;
    display: flex;
    justify-content: space-between;
    height: 100%;

    .header-wrapper-right {
      position: absolute;
      top: 0;
      right: 0;
      width: 50%;
      height: 100%;
      background: $primaryColor;
    }
  }

  .header {
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: $contentWidth;
    height: $headerHeight;
    z-index: 9;

    .left {
      display: flex;
      align-items: center;

      .logo {
        width: 50px;
        height: 50px;
        line-height: 50px;
        border-radius: 50%;
        background: $primaryColor;
        color: #fff;
        font-size: 12px;
        text-align: center;
      }

      .left-right {

        .row1 {
          font-size: 14px;
        }

        .row2 {
          font-size: 12px;
        }
      }
    }

    .nav {
      display: flex;
      align-items: center;
      height: 100%;
      color: #fff;
      text-align: center;
      font-size: 14px;

      .nav-item {
        transition: $transitionTime;
        position: relative;
        width: 120px;
        height: 100%;
        line-height: $headerHeight;
        background: $primaryColor;
        cursor: pointer;

        &:after {
          content: '';
          position: absolute;
          width: 2px;
          height: 60px;
          top: 10px;
          right: 0;
          background: $secondColor;
        }

        .mask {
          position: absolute;
          width: 120px;
          top: $headerHeight;
          box-sizing: border-box;
          border-left: 1px solid $secondColor;
          z-index: 9;
          background: #fff;
          color: #000;

          .mask-item {
            height: 40px;
            line-height: 40px;
            text-align: left;

            &:hover {
              background: $secondColor;
              color: #fff;
            }
          }
        }
      }

      .login {
        position: relative;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 120px;
        height: 100%;
        background: $primaryColor;

        .iconfont {
          font-size: 22px;
        }

        .avatar {
          display: inline-block;
          height: 30px;
          width: 30px;
          border-radius: 50%;
          background: no-repeat center;
          background-size: cover;
        }

        .text {
          font-size: 12px;

          span:hover {
            opacity: .7;
          }
        }

        .mask {
          position: absolute;
          width: 120px;
          top: $headerHeight;
          box-sizing: border-box;
          border-left: 1px solid $secondColor;
          z-index: 9;
          background: #fff;
          color: #000;

          .mask-item {
            height: 40px;
            line-height: 40px;
            text-align: left;

            &:hover {
              background: $secondColor;
              color: #fff;
            }
          }
        }
      }
    }
  }
</style>
