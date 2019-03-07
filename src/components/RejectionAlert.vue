<template>
  <div>
    <el-button type="text" @click="centerDialogVisible = true;textarea=''">Reject</el-button>
    <el-dialog
      :visible.sync="centerDialogVisible"
      width="30%"
      offsetLeft="10px"
      :center=true
    >
      <div class="center-in-center title">
        <span><i class='el-icon-circle-close-outline alerticon'></i></span>
        <br>
        <span class="alerttitle">Reject the following claim entry?</span>
      </div>
      <div class="metadata">
        <div class="alertdiv">
          <div class="floatdiv1">
            <span class="formlabel">Category</span>
            <br>
            <span class="formcontent">{{tableData.category}}</span>
          </div>
          <div class="floatdiv2">
            <span class="formlabel">Amount</span>
            <br>
            <span class="formcontent">${{tableData.amount}}</span>
          </div>
        </div>
        <div class="alertdiv">
          <div class="floatdiv1">
            <span class="formlabel">Date</span>
            <br>
            <span class="formcontent">{{tableData.date}}</span>
          </div>
        </div>
        <div class="alertdiv">
          <div class="floatdiv1">
            <span class="formlabel">From</span>
            <br>
            <span class="formcontent">{{tableData.from}}</span>
          </div>
          <div class="floatdiv2">
            <span class="formlabel">To</span>
            <br>
            <span class="formcontent">{{tableData.to}}</span>
          </div>
        </div>
      </div>
      <div class="remark margintop20">
        <span class="labelremark marginbottom5">Remark</span>
        <br>
        <span
          class="remarkhint marginbottom5">Explain why the claim is being rejected. This will be shown to staff.</span>
        <br>
        <el-input
          class="margintop5 marginbottom5"
          type="textarea"
          maxlength="255"
          autosize="true"
          :autosize="{ minRows: 3 }"
          v-model="textarea">
        </el-input>
        <br>
        <span class="remarkhint marginbottom5">{{255-textarea.length}} characters remaining.</span>
      </div>
      <div class="buttons">
      <span slot="footer" class="dialog-footer">
      <el-button class="floatbutton" type="danger" round @click="confirmReject">Reject</el-button>
      <el-button class="floatbutton" round @click="cancelReject">Cancel</el-button>
      </span>
      </div>
    </el-dialog>
  </div>
</template>

<script>
  export default {
    name: "RejectionAlert",
    props: ['tableData'],
    data() {
      return {
        textarea: '',
        centerDialogVisible: false,
      };
    },
    methods: {
      confirmReject() {
        this.$confirm('This claim will be rejected, confirm?', 'Alert', {
          confirmButtonText: 'Confirm',
          cancelButtonText: 'Cancel',
          type: 'warning'
        }).then(() => {
          this.$message({
            type: 'success',
            message: 'Claim is rejected successfully!'
          });
          this.centerDialogVisible = false;
        }).catch(() => {

        });
      },
      cancelReject() {
        this.$message({
          type: 'info',
          message: 'Rejection is cancelled'
        });
        this.centerDialogVisible = false;
      }
    }
  }
</script>

<style scoped>
  el-dialog {
    position: absolute;
    top: 50%;
    left: 50%;
    margin: 0 !important;
    transform: translate(-50%, -50%);
    text-align: center;
  }

  .alerttitle {
    font-size: 25px;
    color: blue;
  }

  .alerticon {
    font-size: 55px;
    color: red;
  }

  .alertdiv {
    margin: 0 auto;
    padding-bottom: 20px;
    padding-top: 20px;
  }

  .center-in-center {
    text-align: center;
  }

  .formlabel {
    font-family: Montserrat;
    font-size: medium;
    color: #757575;
  }

  .formtext {
    font-family: Montserrat;
    font-size: 16px;
    color: #212121;
  }

  .floatdiv1 {
    position: relative;
    margin-left: 25%;
    float: left;
  }

  .floatdiv2 {
    position: absolute;
    margin-left: 50%;
    float: left;
  }

  .labelremark {
    font-family: Montserrat;
    font-size: large;
    color: #004087;
  }

  .remarkhint {
    font-family: sans-serif;
    font-size: 12px;
    color: #757575;
  }

  .margintop20 {
    margin-top: 20px;
  }

  .margintop5 {
    margin-top: 5px;
  }

  .marginbottom5 {
    margin-bottom: 5px;
  }

  .floatbutton {
    margin-top: -30px;
    margin-right: 10px;
    float: right;
  }
  .buttons{
    margin-top: 30px;
  }
</style>
