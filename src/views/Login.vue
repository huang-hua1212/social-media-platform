<template>
  <div class="background">
    <div class="box">
      <div class="LeftImg"><img src="../../svg/img.svg" alt="Loading..." /></div>
      <div class="RightForm">
        <div class="title"><h>MetalWall</h></div>
        <div class="subTitle"><h>_到元宇宙展開全新社團_</h></div>
        <Form v-slot="{ errors }" id="form" class="form" @submit="toCheckoutPayment2">
          <div class="email-div">
            <Field
              type="email"
              name="email"
              class="email-input"
              v-model="email"
              rules="required|email"
              :class="{ 'is-invalid': errors['email'] }"
              placeholder="Email"
              @keyup.prevent="isBtnSendOutActive()"
            ></Field>
          </div>
          <div class="password-div">
            <Field
              type="password"
              name="password"
              class="password-input"
              v-model="password"
              rules="required"
              :class="{ 'is-invalid': errors['password'] }"
              placeholder="Password"
              @keyup.prevent="isBtnSendOutActive()"
            ></Field>
          </div>
          <div class="errorDisplay">
            <error-message name="email" class="invalid-feedback emailErrMessage"></error-message>
            <br /><error-message
              name="password"
              class="invalid-feedback emailErrMessage"
            ></error-message>
          </div>
          <div class="btn-OuterDiv">
            <a
              type="button"
              :class="{ 'sendOutA-Active': isSendOutActive }"
              class="sendOutA"
              @click.prevent="login()"
              href="#"
              ><div class="sendOutBtn-Div" :class="{ 'sendOutBtn-Div-Active': isSendOutActive }">
                登入
              </div></a
            >
          </div>
        </Form>
        <div class="btn-register-div">
          <a class="btn-register-a" type="button" href="#" @click.prevent="">註冊帳號</a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios';

export default {
  data() {
    return {
      isSendOutActive: false,
      email: '',
      password: '',
    };
  },
  created() {},
  methods: {
    isBtnSendOutActive() {
      if (this.email && this.password) {
        this.isSendOutActive = true;
      } else {
        this.isSendOutActive = false;
      }
    },
    login() {
      // TEST
      const url = `${process.env.VUE_APP_API}/user/login`;
      // const url = `${process.env.VUE_APP_API}/users/sign_in`;

      const data = {
        username: this.email,
        password: this.password,
      };
      axios
        .post(url, data)
        .then((res) => {
          // 儲存cookie
          document.cookie = `hexToken=${res.data.token}; expired=${res.data.token_expiresAt};`;
          // document.cookie = `hexToken=12345; expired=${res.data.token_expiresAt};`;

          this.$router.push('/posts-with-comments');
        })
        .catch((err) => {
          console.dir(err);
        });
    },
  },
};
</script>
<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Paytone+One&display=swap');

.background {
  word-break: break-all;
  display: flex;
  justify-content: center;
  width: 100%;
  height: 100%;
  background: #efece7;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  padding-top: 6%;
}
.box {
  border: black solid;
  display: flex;
  width: auto;
  height: 24em;
  padding-left: 3%;
  padding-right: 3%;
  padding-top: 2%;
  padding-bottom: 3%;
  box-shadow: -8px 8px 0px #00040029;
}
.LeftImg {
  margin-top: 1.5em;
}
.RightForm {
  margin-left: 4em;
  text-align: center;
}
.title > h {
  font-size: 3.75em;
  font-family: 'Paytone One', sans-serif;
  font-weight: bold;
}
.subTitle > h {
  font-size: 1.1em;
  font-family: 'Paytone One', sans-serif;
  font-weight: bold;
}
// 為了讓error absolute位置(不占空間，卻又絕對)
.form {
  position: relative;
}
.email-div {
  margin-top: 9%;
}
.email-div input {
  border: black solid;
  width: 100%;
  height: 2em;
  padding-left: 0.2em;
  font-size: 1.2em;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
.errorDisplay {
  width: 100%;
  position: absolute;
  left: 50%;
  transform: translate(-50%, 0);
  top: 44%;
}
// .emailErrMessage {
//   position: absolute;
//   left: 50%;
//   transform: translate(-50%, 0);
//   top: 44%;
// }
.password-div {
  width: 100%;
  margin-top: 5%;
  // margin-top: 12%;
  // margin-top: 15%;
}
.password-div input {
  border: black solid;
  width: 100%;
  height: 2em;
  padding-left: 0.2em;
  font-size: 1.2em;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
.btn-OuterDiv {
  margin-top: 25%;
  // margin-top: 18%;
  margin-bottom: 0;
}
a {
  text-decoration: none;
}
.sendOutA {
  pointer-events: none;
}
.sendOutBtn-Div {
  background: #a8b0b9;
  border: #808080 solid;
  border-radius: 0.5em;
  color: white;
  padding-top: 2.8%;
  padding-bottom: 2.8%;
  text-align: center;
  font-size: 1.1em;
}
.sendOutA-Active {
  pointer-events: auto;
}
.sendOutBtn-Div-Active {
  background: #03438d;
  border: black solid;
  border-radius: 0.5em;
  box-shadow: -0.2em 0.2em 0em 0 black;
  color: white;
  padding-top: 2.8%;
  padding-bottom: 2.8%;
  text-align: center;
  font-size: 1.1em;
}
.btn-register-div {
  margin-top: 0.5em;
}
.btn-register-div a {
  color: black;
}
</style>
