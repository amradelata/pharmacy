<template>
  <div class="signIn">
    <div class="overlay">
      <div class="signIncards">
        <div class="signIncard">
          <!-- <p class="is-size-1 head">صيدلية</p>
          <p class="is-size-3">اول موقع لتوصيل الأدويه فى العالم العربى</p>-->
          <!-- <img src="https://static.dribbble.com/users/1081436/screenshots/4026839/untitled-3.jpg" /> -->
          <div class="myimg"></div>
        </div>
        <div class="signIncard myquestion">
          <p class="is-size-1 head">صيدلية</p>
          <p class="is-size-2 has-text-black">اول موقع لتوصيل الأدويه فى العالم العربى</p>
          <p class="is-size-2 has-text-black">هل لديك حساب ؟</p>
          <!--putons  -->
          <div class="mybuttons">
            <nuxt-link to="/typelogin">
              <button class="button is-primary is-medium">نعم , لدى حساب بالفعل</button>
            </nuxt-link>

            <nuxt-link to="/typesignin">
              <button class="button is-primary is-medium">لا , اود انشاء حساب</button>
            </nuxt-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
const usersArray = "https://pharmacy-databeas.herokuapp.com/user-information";
export default {
  data() {
    return {
      password: "",
      email: "",
      lastName: "",
      firstName: "",
      userstat: ""
    };
  },
  methods: {
    usercustomer() {
      this.userstat = "oner";

      console.log(this.userstat);
    },
    useroner() {
      this.userstat = "customer";
      console.log(this.userstat);
    },
    async submit() {
      const nameres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/user-information/?firstName=${this.firstName}`
      );
      if (nameres.data.length > 0) {
        alert("هذا الاسم موجود بالفعل ");
        return;
      }
      const res = await axios.post(usersArray, {
        firstName: this.firstName,
        lastName: this.lastName,
        email: this.email,
        password: this.password,
        userstat: this.userstat
      });

      localStorage.setItem("status", "loggedIn");
      localStorage.setItem("userfirstName", this.firstName);
      localStorage.setItem("userlastName", this.lastName);
      localStorage.setItem("useremail", this.email);
      localStorage.setItem("userpassword", this.password);
      localStorage.setItem("userstat", this.userstat);

      const useracount = localStorage.getItem("userstat");
      if (useracount == "customer") {
        this.$router.replace("/drugs");
      } else if (useracount == "oner") {
        this.$router.replace("/signInOner2");
      }
    }
  }
};
</script>

<style  scoped>
.signIn {
  position: absolute;
  top: 50%;
  bottom: 0;
  right: 0;
  left: 0;
  transform: translate(0, -50%);
}

.head {
  color: #00d1b2;
}
.signIncards {
  display: flex;
  flex-wrap: wrap;
  margin-right: 20px;
}
.myimg {
  height: 100%;
  width: 100%;
  /* <img src="~/assets/img/loding.gif" /> */
  background-image: url("https://static.dribbble.com/users/992274/screenshots/6278477/composition_with_little_men_kit8-net.png");
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
}
.myquestion {
  /* margin-top: 10% !important; */
}

.signIncard {
  text-align: center;
  flex-basis: calc(50% - 20px);
  display: inline-block;
  background-color: transparent;
  margin: 10px;
  padding: 10px;
  color: #fff;
}

.mybuttons {
  margin-top: 30px;
}
.mybuttons button {
  margin-right: 35px;
  width: 250px;
}

@media screen and (max-width: 768px) {
  .signIncard {
    flex-basis: calc(100% - 10px);
  }
  .mybuttons button {
    margin-right: 0;
    margin-top: 20px;
  }
  .signIncards {
    margin-right: 0;
  }
  .myimg {
    height: 300px;
    display: inline-block;
  }
  .signIn {
    position: absolute;
    top: 0%;
    bottom: 0;
    right: 0;
    left: 0;
    transform: translate(0, -0%);
  }
}
</style>