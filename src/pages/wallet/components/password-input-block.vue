<template>
  <div class="password-block item-block">
    <van-cell-group :border="false">
      <pl-password-strength
        v-model="form.walletPwd"
        :type="inputType"
        :data-vv-as="$t('wallet.setTranPwdPlaceholder')"
        :placeholder="$t('wallet.setTranPwdPlaceholder')"
        v-validate="'required|min:6'"
        name="walletPwd"></pl-password-strength>
      <van-field
        v-model="form.confirmWalletPwd"
        maxlength="50"
        :type="inputType"
        :data-vv-as="$t('wallet.setTranPwdPlaceholder2')"
        :placeholder="$t('wallet.setTranPwdPlaceholder2')"
        v-validate="'required|min:6'"
        :icon="inputIcon"
        name="confirmWalletPwd"
        @click-icon="transferPwdMode">
      </van-field>
    </van-cell-group>
  </div>
</template>
<script>
  export default {
    props: {
      value: {
        type: Object,
        default: () => {
          return {
            walletPwd: '',
            confirmWalletPwd: ''
          };
        },
      }
    },
    watch: {
      value (val) {
        this.from = val;
      },
      form (val) {
        this.$emit('input', val);
      }
    },
    data () {
      return {
        form: this.value,
        inputType: 'password',
        inputIcon: 'password-not-view',
      };
    },
    methods: {
      transferPwdMode () {
        if (this.inputType === 'password') {
          this.inputType = 'text';
          this.inputIcon = 'password-view';
        } else {
          this.inputType = 'password';
          this.inputIcon = 'password-not-view';
        }
      },
      resetForm () {
        this.inputType = 'password';
        this.inputIcon = 'password-not-view';
        this.form.walletPwd = '';
        this.form.confirmWalletPwd = '';
      }
    }
  };
</script>
<style lang="scss" rel="stylesheet/scss" scoped></style>
<style lang="scss" rel="stylesheet/scss">
  .password-block {
    .van-field {
      height: 56px;
    }
  }
</style>
