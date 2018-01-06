<template>
  <modal @close="handleClose">
    <section class="login-modal">
      <div class="title c-font-big">
        <div
          class="tab-sign-in c-btn "
          :class="{
            'selected':currentTab === 0
          }"
          @click="handleTabChange(0)">
          登录
        </div>
        <div class="divider c-gap-left-small c-gap-right-small">|</div>
        <div
          class="tab-sign-up c-btn"
          :class="{
            'selected':currentTab === 1
          }"
          @click="handleTabChange(1)">
          注册
        </div>
      </div>

      <section class="bottom sign-in">
        <!--账号-->
        <section class="form-item">
          <div class="c-font-big">电子邮箱 / 手机号码</div>
          <el-input
            class="c-gap-top"
            v-model="form.username"></el-input>
          <div
            v-if="currentTab === 0"
            class="row-right c-gap-top">
            <span class="link c-btn">
              忘记用户名？
            </span>
          </div>
        </section>
        <!--密码-->
        <section class="form-item c-gap-top-20">
          <div class="c-font-big">密码</div>
          <el-input
            class="c-gap-top"
            v-model="form.password">
          </el-input>
          <div
            v-if="currentTab === 0"
            class="row-right c-gap-top">
            <span class="link c-btn">
              忘记密码？
            </span>
          </div>
          <div
            v-if="currentTab === 1"
            class="c-color-grey c-gap-top">
            (6个字/数字以上，不包括空格)
          </div>
        </section>
        <!--确认密码-->
        <section
          v-if="currentTab === 1"
          class="form-item c-gap-top-20">
          <div class="c-font-big">确认密码</div>
          <el-input
            class="c-gap-top"
            v-model="form.passwordAgain">
          </el-input>
        </section>
        <!--按钮1-->
        <el-button
          v-if="currentTab === 0"
          class="btn-sign-in"
          type="success">
          登录
        </el-button>
        <!--按钮2-->
        <el-button
          v-if="currentTab === 1"
          class="btn-sign-in"
          type="success">
          注册
        </el-button>
      </section>

    </section>
  </modal>
</template>

<script>
  import Modal from './Modal.vue';

  export default {
    name: 'FinancialCalculatorModal',
    data() {
      return {
        currentTab: 0,  // 当前状态；登录还是注册
        form: {
          username: '',
          password: '',
          passwordAgain: ''
        },
      }
    },
    components: {
      Modal
    },
    methods: {
      handleClose() {
        this.$emit('close');
      },
      handleTabChange(index) {
        console.log(index);
        this.currentTab = index;
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import "../assets/app.scss";

  .login-modal {
    padding: 0 20px 40px;
    width: 500px;
    overflow-y: auto;
    overflow-x: hidden;
    box-sizing: border-box;

    .title {
      display: flex;
      justify-content: center;

      .tab-sign-in, .tab-sign-up {
        padding: 0 10px;
      }

      .selected {
        background: $primaryColor;
        color: #fff;
      }
    }

    .bottom {
      margin-top: 60px;

      .form-item {
        position: relative;

        .row-right {
          position: absolute;
          bottom: -30px;
          right: 0;
          text-align: right;

          .link {
            color: $lightBlue500;
          }
        }
      }

      .btn-sign-in {
        margin-top: 60px;
        width: 100%;
      }
    }
  }

</style>
