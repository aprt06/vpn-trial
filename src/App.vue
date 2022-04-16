<template>
  <div class="common-layout">
  
    <el-container>
      <el-header id="navheader">
        <el-row align="middle" justify="center"  >
          <h3 >LUNAR KINGDOM - Lunar Thailand VPN - Trial</h3>

         </el-row>
      </el-header>
      <el-main>
          <el-row  justify="center">
          <img src="./assets/lunar-pay.png">

          </el-row>

 <el-row justify="center">
    
   <el-form
    ref="formRef"
    :model="dynamicValidateForm"
    label-width="120px"
    class="demo-dynamic"
  >
   <el-form-item><h4 class="font-bold">VPN file Trial 2 days</h4></el-form-item>
    <!-- <el-form-item>
       <el-select v-model="value" class="m-2" size="large">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value"
    />
  </el-select>
  </el-form-item> -->
   
    <el-form-item
      prop="email"
      label="Email"
      :rules="[
        {
          required: true,
          message: 'Please input email address',
          trigger: 'blur',
        },
        {
          type: 'email',
          message: 'Please input correct email address',
          trigger: ['blur', 'change'],
        },
      ]"
    >
      <el-input v-model="dynamicValidateForm.email" />
    </el-form-item>
    
     <el-form-item>
     
      <el-button type="primary" @click="submitForm(formRef)">Submit</el-button>
      
    </el-form-item>
  </el-form>
    </el-row>
  <el-row >
        ** Vpn file will attach with your email

  </el-row>
      </el-main>
      <el-footer>
        <el-row justify="space-evenly">
          <img src="./assets/ksher.png"  />
          <img src="./assets/truemoney.png"  > 
          <img src="./assets/pp.jpg" > 
          <img src="./assets/rabbit.png" > 
          <img src="./assets/alipay.png" > 
          <img src="./assets/wechat.png"   > 
  
    

        </el-row>
       
        <el-row justify="end">
          <h4  class="font-bold">Lunar-Kingdom Copyright © 2022</h4>  
          <a href="https://www.trustmarkthai.com/callbackData/popup.php?data=a8a480199-39-5-48523e48a99d887e3a53d7c00d89dc82377c">
          <img src="./assets/bns_registered.jpg" style="margin-left:2rem;">
          </a>
        </el-row>
      </el-footer>
    </el-container>
  </div>
 
   
</template>




 <script lang='ts' setup>
import { RouterLink, RouterView } from 'vue-router'
//import HelloWorld from '@/components/HelloWorld.vue'

import { reactive, ref } from 'vue'
import type { FormInstance } from 'element-plus'
import axios from 'axios'
 

function callApi(email,amount){

 
const data = { 'email': email,'amount':amount };
const url = 'https://35bd-94-74-116-50.ngrok.io/.netlify/functions/server/order-ksher'
const params = new URLSearchParams()
params.append('email', email)
params.append('amount', amount)
const config = {
  headers: {
    'Content-Type': 'application/x-www-form-urlencoded'
  }
}
axios.post(url,params,config).then((response)=>{

   window.location.href = response.data.url;
}).catch((err)=>{
  console.log(err)
})
}

const value = ref('')

const options = [
  {
    value: '1 Month',
    label: 'Package',
  },
]

const formRef = ref<FormInstance>()
const dynamicValidateForm = reactive<{
   
  email: string
}>({
   
  email: '',
})
 

const submitForm = (formEl: FormInstance | undefined) => {
  if (!formEl) return
  formEl.validate((valid) => {
    if (valid) {
      //console.log('submit!')
      //console.log(dynamicValidateForm.email)
      const email = dynamicValidateForm.email
      callApi(email,9900)

    } else {
      console.log('error submit!')
      return false
    }
  })
}

const resetForm = (formEl: FormInstance | undefined) => {
  if (!formEl) return
  formEl.resetFields()
}
</script>
export default {
  name: 'App',
  metaInfo: {
    title: 'Default App Title',
    titleTemplate: '%s | vue-meta Example App',
    htmlAttrs: {
      lang: 'en-US'
    },
    meta: [
      { charset: 'utf-8' },
      { name: 'description', content: 'An example Vue application with vue-meta.' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' }
    ]
  },
  // ...
}
<style>
@import '@/assets/base.css';

#app {
   margin: 0 auto;
  padding: 0rem;

 }
#navheader{
  padding-top: 1rem;
  background-color: #051344;
 
}
#navheader {
  color:white;
}
footer{
  
  position: relative;
  justify-content: center;
   
 }
footer img{
  width:130px;
  height:100%;


}
.font-bold{
  font-weight: 500;
}
.el-footer{
    background-color: #01cdcd;
    bottom: 0;
    position: relative;
    width: 100%;
    height: auto !important;
    padding-top:2rem !important;
    color:white
}
</style>

