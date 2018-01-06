<template>
  <modal @close="handleClose">
    <section class="financial-calculator">
      <div class="title c-font-20">月供粗算</div>
      <div class="row2">{{monthlyInstallmentPaymentRough}}</div>
      <section
        v-for="(item, index) in list"
        :key="index"
        class="item c-gap-top-20">
        <div
          class="row1 c-flex">
          <div class="left">{{item.label}}</div>
          <div class="right c-flex">
            <el-input
              v-model="form[item.formName]">
            </el-input>
            <span
              class="unit c-gap-left-20">
              {{item.unit}}
            </span>
          </div>
        </div>
        <el-slider v-model="form[item.formName]"></el-slider>
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
        monthlyInstallmentPaymentRough: '￥2000.00', // 月供粗算
        form: {
          carPrice: 36, // 汽车价格
          downPayment: 42,  // 首付
          substitution: 56, // 置换
          purchaseTax: 12, // 购置税
          luxuryCarPurchaseTax: 24, // 豪车购置税
          interestRate: 98, // 利率
          loansPeriod: 34, // 贷款周期
        },
        list: [
          {
            label: '汽车价格',
            formName: 'carPrice',
            unit: 'RMB'
          },
          {
            label: '首付',
            formName: 'downPayment',
            unit: '%'
          },
          {
            label: '置换',
            formName: 'substitution',
            unit: '%'
          },
          {
            label: '购置税',
            formName: 'purchaseTax',
            unit: '%'
          },
          {
            label: '豪车购置税',
            formName: 'luxuryCarPurchaseTax',
            unit: '%'
          },
          {
            label: '利率',
            formName: 'interestRate',
            unit: '%'
          },
          {
            label: '贷款周期',
            formName: 'loansPeriod',
            unit: '月'
          }
        ]
      }
    },
    components: {
      Modal
    },
    methods: {
      handleClose() {
        this.$emit('close');
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import "../assets/app.scss";

  .financial-calculator {
    padding: 0 20px;
    width: $modalWidth;
    height: $modalHeight;
    overflow-y: auto;
    overflow-x: hidden;
    text-align: center;
    box-sizing: border-box;
  }

  .item {

    .row1 {
      justify-content: space-between;

      .unit {
        width: 40px;
      }
    }
  }
</style>
