<template>
  <div class="mui-content-padded">
    <div class="form-group">
      <div class="img-box"><img src="../assets/img/logo.png"></div>
    </div>
    <form class="mui-input-group add-form">
      <div class="mui-input-row">
        <label>姓名</label>
        <input type="text" placeholder="请输入姓名" v-model="postCard.name">
      </div>
      <div class="mui-input-row">
        <label>手机</label>
        <input type="text" placeholder="请输入手机" v-model="postCard.phone">
      </div>
      <div class="mui-input-row">
        <label>QQ</label>
        <input type="text" placeholder="请输入QQ" v-model="postCard.qq">
      </div>
      <div class="mui-input-row">
        <label>标签</label>
        <input type="text" placeholder="请输入标签" v-model="postCard.tag">
      </div>
      <div class="mui-button-row">
        <button type="button" class="mui-btn mui-btn-primary mui-btn-block" v-on:click="submitForm">提交</button>
      </div>
    </form>
  </div>

</template>
<script>
  import Store from '../store'
    export default {
        data () {
            return {
                postCard:{
                    id:"",
                  name:"",
                  phone:"",
                  qq:"",
                  tag:""
                }
            }
        },
      methods:{
            submitForm:function () {
                if(this.validPostCard()){
                    this.postCard.id=new Date().getTime();
                  Store.savePostCard(this.postCard);
                 this.$messagebox.alert('保存成功！').then(function () {
                   window.location.href="#/list";
                 })
                }
            },
          validPostCard:function () {
            var phoneReg=/^1[3|4|5|7|8][0-9]{9}$/;
            var qqReg=/^\d{5,10}$/;
            var postCard=this.postCard;
            if(postCard.name==''){
              this.$toast({
                message: '请输入姓名',
                position: 'bottom',
                duration: 1000
              });
                return false
            }
            if(!phoneReg.test(postCard.phone)){
              this.$toast({
                message: '请输入正确的手机号',
                position: 'bottom',
                duration: 1000
              });
              return false
            }
            if(!qqReg.test(postCard.qq)){
              this.$toast({
                message: '请输入正确的QQ号',
                position: 'bottom',
                duration: 1000
              });
              return false
            }
            if(postCard.tag==''){
              this.$toast({
                message: '请输入标签',
                position: 'bottom',
                duration: 1000
              });
              return false
            }
            return true;
          }
      }
    }
</script>
