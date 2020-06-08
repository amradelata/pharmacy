<template>
  <div>
    <!-- user states -->
    <div class="home">
      <div class="hometext">
        <!-- inptus -->
        <div class="field">
          <div class="control">
            <nuxt-link to="/logIn">
              <button class="button is-primary is-outlined">تسجيل الدخول</button>
            </nuxt-link>

            <nuxt-link to="/signIn">
              <button class="button is-primary is-outlined">حساب جديد</button>
            </nuxt-link>
            <input class="input is-primary" type="text" placeholder="اسمك" v-model="firstName" />
            <input
              class="input is-primary"
              type="text"
              placeholder="اسم العائلة"
              v-model="lastName"
            />
            <input
              class="input is-primary"
              type="text"
              placeholder="الرقم السرى"
              v-model="password"
            />
            <input
              class="input is-primary"
              type="text"
              placeholder="البريد الالكترونى"
              v-model="email"
            />

            <!--  -->
            <div class="control">
              <p>نوع الحساب</p>
              <label class="radio">
                <input type="radio" name="foobar" @click="useroner()" />
                <p class="is-size-6">مشترى</p>
              </label>
              <label class="radio">
                <input type="radio" name="foobar" @click="usercustomer()" />
                <p class="is-size-6">مالك صيدلية</p>
              </label>
            </div>
            <!--  -->
            <button class="button is-primary" @click="submit()">حساب جديد</button>
          </div>
        </div>

        <!-- inptus -->
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
        this.$router.replace("/customer");
      } else if (useracount == "oner") {
        this.$router.replace("/pharmacyowner");
      }
    }
  }
};
</script>

<style  scoped>
.home {
  text-align: center;
  position: relative;
  height: 100vh;
  width: 100vw;
}
.home input {
  margin: 15px 0;
}
.home p {
  margin-bottom: 25px;
  color: aliceblue;
}
.mideltext {
  font-size: 45px;
  color: aliceblue;
  margin: 0 35px;
}
.hometext {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.radio {
  text-align: center;
  margin: 0 25px;
}
@media screen and (max-width: 768px) {
  .mideltext {
    display: block;
    margin: 35px;
  }
}
</style>