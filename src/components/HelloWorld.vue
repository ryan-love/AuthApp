<template>
<div>
  <div class="hello" ref="qr">
  </div>

</div>
</template>

<script>
import * as OTPAuth from 'otpauth';
import QRCodeStyling from 'qr-code-styling';
export default {
  name: 'HelloWorld',
  data(){
    return{
  totp:new OTPAuth.TOTP({
	secret:'WIP56LGAIKOPCAUX'.split(" ").join(""),
  })
    }
  }, 
  methods:{
    test(){

    


// Generate a token.
let token = this.totp.generate();
console.log(token)

console.log(this.totp)
let delta = this.totp.validate({
	token: token,
	window: 1
});

console.log(delta)

// Convert to Google Authenticator key URI.
// otpauth://totp/ACME:AzureDiamond?issuer=ACME&secret=NB2W45DFOIZA&algorithm=SHA1&digits=6&period=30
let uri = this.totp.toString(); // or "OTPAuth.URI.stringify(totp)"
console.log(uri)
const qrCode = new QRCodeStyling({
        width: 300,
        height: 300,
        type: "svg",
        data: uri,
        image: "https://upload.wikimedia.org/wikipedia/commons/5/51/Facebook_f_logo_%282019%29.svg",
        dotsOptions: {
            color: "#4267b2",
            type: "rounded"
        },
        backgroundOptions: {
            color: "#e9ebee",
        },
        imageOptions: {
            crossOrigin: "anonymous",
            margin: 20
        }
    });
// Convert from Google Authenticator key URI.
let parsedTotp = OTPAuth.URI.parse(uri);
console.log(parsedTotp)
 qrCode.append(this.$refs.qr);




    },
    generate(){
this.totp.generate();
    },
    qr(){

    }
  },
  mounted(){
    this.test()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
