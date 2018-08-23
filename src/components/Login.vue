<template>
<div class="login">
  <div :class="['form', {'expand': isRegisterTabActive}]">
    <div class="header">
      <div @click="switchTo('loginTab')" :class="['tab', {'active' : isLoginTabActive}]">
        <div class="title">Login</div>
      </div>
      <div @click="switchTo('registerTab')" :class="['tab', {'active' : isRegisterTabActive}]">
        <div class="title">Register</div>
      </div>
    </div>
    <div v-show="isLoginTabActive" class="login-area page">
      <div class="email">
        <input v-model="email" id="email" placeholder="Email" spellcheck="false" autocomplete="off" />
        <div class="progress-bar">
          <div>
            {{email}}
          </div>
        </div>
      </div>
      <div class="password">
        <input v-model="password" id="password" placeholder="Password" type="password" spellcheck="false" autocomplete="off" />
        <div class="progress-bar">
          <div>
            {{password}}
          </div>
        </div>
      </div>
      <div id="signin" :class="{'available': canSignIn}" @click="login()">Sign in</div>
    </div>
    <div v-show="isRegisterTabActive" class="register-area page">
      <div class="email">
        <input v-model="registerEmail" id="registerEmail" placeholder="Email" spellcheck="false" autocomplete="off" />
        <div :class="['progress-bar', {'valid': checkRegisterEmail}]">
          <div>
            {{registerEmail}}
          </div>
        </div>
      </div>
      <div class="password">
        <input v-model="registerPassword" id="registerPassword" placeholder="Password" type="password" spellcheck="false" autocomplete="off" />
        <div :class="['progress-bar', {'valid': passwordsMatch}]">
          <div>
            {{registerPassword}}
          </div>
        </div>
      </div>
      <div class="password">
        <input v-model="registerPassword2" id="registerPassword2" placeholder="Confirm Password" type="password" spellcheck="false" autocomplete="off" />
        <div :class="['progress-bar', {'valid': passwordsMatch}]">
          <div>
            {{registerPassword2}}
          </div>
        </div>
      </div>
      <div id="signup" :class="{'available': canSignUp}">Sign up</div>
    </div>
  </div>
  <Canvas></Canvas>
</div>
</template>

<script>
import Canvas from "./Canvas.vue";

export default {
  name: "Login",
  methods: {
    switchTo: function(tab) {
      if (tab === "loginTab") {
        this.isLoginTabActive = true;
        this.isRegisterTabActive = false;
      } else {
        this.isLoginTabActive = false;
        this.isRegisterTabActive = true;
      }
    },
    login: function() {
      this.$router.push("/home");
    }
  },
  computed: {
    checkEmail: function() {
      return this.emailRegex.test(this.email);
    },
    checkRegisterEmail: function() {
      return this.emailRegex.test(this.registerEmail);
    },
    passwordsMatch: function() {
      return (
        this.registerPassword === this.registerPassword2 &&
        this.registerPassword.length > 0
      );
    },
    canSignIn: function() {
      return this.checkEmail && this.password.length > 0;
    },
    canSignUp: function() {
      return this.checkRegisterEmail && this.passwordsMatch;
    }
  },
  data() {
    return {
      isLoginTabActive: true,
      isRegisterTabActive: false,
      email: "",
      password: "",
      registerEmail: "",
      registerPassword: "",
      registerPassword2: "",
      emailRegex: /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
    };
  },
  components: {
    Canvas: Canvas
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.login {
  width: 100%;
  height: 100%;
  background: #ff5f6d;
  background: -webkit-linear-gradient(to left, #ffc371, #ff5f6d);
  background: linear-gradient(to left, #ffc371, #ff5f6d);
  align-items: center;
  justify-content: center;

  .form {
    width: 320px;
    height: 320px;
    background: white;
    border-radius: 10px;
    overflow: hidden;
    transition: height 0.1s ease;
    z-index: 99999999;

    &.expand {
      height: 390px;
    }

    .header {
      flex: 1;
      max-height: 50px;
      flex-direction: row;
      justify-content: space-evenly;

      .tab {
        flex: 1;
        align-items: center;
        justify-content: center;
        background: #eaeaea;
        cursor: pointer;
        color: #777;

        &.active {
          background: white;
          color: #333;
        }
      }
    }

    .page {
      flex: 1;
      align-items: center;
      justify-content: space-evenly;

      input {
        border: none;
        outline: none;
        height: 50px;
        color: #333;
        font-size: 20px;
        width: 250px;
      }

      .progress-bar {
        display: inline-flex;
        height: 2px;
        background: #ececec;
        overflow: hidden;
        width: 250px;

        &.valid {
          div {
            background: #48c148;
          }
        }

        div {
          height: 100%;
          width: fit-content;
          background: #333;
          font-size: 20px;
          overflow: hidden;
          transition: all 0.5s ease;
        }
      }

      #signin,
      #signup {
        background: #333;
        width: 235px;
        padding: 10px;
        border-radius: 5px;
        margin-top: 20px;
        color: white;
        cursor: pointer;
        transition: all 0.2s ease;
        pointer-events: none;
        opacity: 0.7;

        &:hover {
          background: #444;
        }

        &.available {
          pointer-events: all;
          opacity: 1;
        }
      }
    }
  }
}
</style>
