<template>
  <div>
    <video ref="qrObj"></video>
    {{qr}}
    {{message}}
    {{totp}}
  </div>
</template>
<script>
import QrScanner from 'qr-scanner'
// import * as OTPAuth from 'otpauth';
export default {
  data(){
    return{
      qr:null,
      qrScanner:null,
      totp:{},
      message:"",
      scan:(result)=>{
        if(result){

        
        if(result.data.split("totp")[0] === "otpauth://"){
          this.qr=result.data
          this.totp.label = result.data.split("totp/")[1].split("?")[0]
          let itr = new URLSearchParams(result.data).entries()
          for (let i = 0; i < array.length; i++) {
            const element = array[i];
            
          }
          
        } else{
          this.message = "QR Code does not contain OTP Address"
        }
        } else{
          this.message = "No Valid Data"
        }
      }
    }
  },
  methods:{
    async checkQrStatus(){
      if(await QrScanner.hasCamera()){
this.qrScanner = new QrScanner(this.$refs.qrObj, this.scan, {
  onDecodeError: error => {
    this.message = error
  },
  highlightScanRegion: true,
  highlightCodeOutline: true,
}).start()
      } else{
        this.message = "No Camera Presented. Please Input Code Manually"
      }
    }
  },
  mounted(){
    this.checkQrStatus()
  }
}
</script>

<style scoped>

</style>