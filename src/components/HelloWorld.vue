<template>
  <v-form v-model="valid">
    <v-container>
      <v-row>

        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>
        </v-col>

        <v-col
          cols="12"
          md="4"
        >
          <v-text-field
            v-model="password"
            :rules="passwordRules"
            :counter="15"
            label="password"
            required
          ></v-text-field>
        </v-col>
      </v-row>
      
      <v-btn

      :disabled ='cheaker'
      v-on:click="logincheak()"
    >
      Login
    </v-btn>
    </v-container>
  </v-form>
  
</template>

<script>
  export default {
    data: () => ({
      valid: false,
      cheaker:true,
      password: '',
      passwordReg:/^[0-9a-zA-Z]+$/,
      passwordRules: [
        v => /^[0-9a-zA-Z]+$/.test(v) || '英数字にしてください',
        v => v.length >= 12 || 'パスワードは12文字以上にしてください',
        v => v.length <= 15 || 'パスワードは15文字以下にしてください',
      ],
      email: '',
      emailReg:/.+@shizuoka.ac.jp+/,
      emailRules: [
        v => !!v || 'メールアドレスを記入してください',
        v => /.+@shizuoka.ac.jp+/.test(v) || 'メールアドレスは@shizuoka.ac.jpである必要があります',
      ],
      userdata:{
        email:"aaa.aaa@shizuoka.ac.jp",
        password:"0123456789ab"
      }
    }),
    methods:{
      logincheak(){
        if(this.password == this.userdata.password && this.email == this.userdata.email){
          alert("ログイン成功");
        }else{
          alert("メールアドレスまたはパスワードが違います")
        }
      }
    },
    watch:{
      email:function(){
        if(this.emailReg.test(this.email) && this.passwordReg.test(this.password) && this.password.length >= 12 && this.password.length <= 15){
          this.cheaker = false;
        }else{
          this.cheaker = true;
        }
      },
      password:function(){
        if(this.emailReg.test(this.email) && this.passwordReg.test(this.password) && this.password.length >= 12 && this.password.length <= 15){
          this.cheaker = false;
        }else{
          this.cheaker = true;
        }
      }
    }
  }
</script>