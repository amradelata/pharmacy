<template>
  <div>
    <!-- user states -->
    <div class="home">
      <div class="hometext">
        <!-- inptus -->
        <div class="field">
          <div class="control">
            <input
              class="input is-primary"
              type="text"
              placeholder="خطوط الطول- موقعك"
              v-model="pharmacyLongitude"
            />
            <input
              class="input is-primary"
              type="text"
              placeholder="حطوط العرض- موقعك"
              v-model="pharmacyLatitude"
            />

            <button class="button is-primary" @click="submit()">تسجيل الدخول</button>
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
      pharmacyLongitude: "",
      pharmacyLatitude: ""
    };
  },
  methods: {
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

      //   localStorage.setItem("status", "loggedIn");
      //   localStorage.setItem("userfirstName", this.firstName);
      //   localStorage.setItem("userlastName", this.lastName);
      //   localStorage.setItem("useremail", this.email);
      //   localStorage.setItem("userpassword", this.password);
      //   localStorage.setItem("userstat", this.userstat);

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