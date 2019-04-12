<template>
  <div class="home">
    <md-field class="input">
      <label>EOS账户名</label>
      <md-input v-model="account"></md-input>
    </md-field>
    <md-field class="input">
      <label>加油码</label>
      <md-input v-model="inviteCode"></md-input>
    </md-field>
    <md-button class="md-primary" @click="getResource">
      <span v-show="!loading">提交</span>
      <span v-show="loading"><md-progress-spinner class="loading" :md-stroke="2" :md-diameter="20"
                                                  md-mode="indeterminate"></md-progress-spinner></span>
    </md-button>
    <md-snackbar :md-active.sync="showMsg">
      <span>{{responseMsg}}</span>
    </md-snackbar>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'Home',
    data() {
      return {
        loading: false,
        account: '',
        inviteCode: '',
        responseMsg: '',
        showMsg: false,
      }
    },
    methods: {
      async getResource() {
        axios.defaults.timeout = 30000;
        axios.defaults.baseURL = 'http://119.29.162.64:3031';
        try {
          if (!this.account) throw new Error('账户名不能为空');
          if (!this.inviteCode) throw new Error('邀请码不能为空');

          this.loading = true;
          const resp = await axios.post('/fuelfilling', {
            account: this.account,
            inviteCode: this.inviteCode,
          });

          if (resp.data.code) {
            throw new Error(resp.data.msg);
          } else {
            this.responseMsg = `成功给${this.account}加油`;
          }
          this.account = '';
          this.inviteCode = '';
        } catch (e) {
          this.responseMsg = e.message;
        } finally {
          this.showMsg = true;
          this.loading = false;
        }
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .home {
    width: 200px;
    margin: 40px auto;
  }

  .input {
    font-size: 14px;
  }

</style>
