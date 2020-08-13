<template>
  <div class="signIn">
    <div class="overlay">
      <div class="signIncards">
        <div class="signIncard slogan">
          <p class="is-size-1 head">صيدلية</p>
          <p class="is-size-3 has-text-black">اول موقع لتوصيل الأدويه فى العالم العربى</p>
        </div>
        <div class="signIncard">
          <div class="myinputs">
            <img
              class="inputimg"
              src="https://static.dribbble.com/users/1769954/screenshots/7367730/media/60163f104190cf8b2097bdba6b0fab5a.png"
              alt
            />
            <p class="is-size-3">من فضلك ادخل البيانات التالية (حساب مشترى)</p>
            <!--putons  -->
            <div class="mybuttons">
              <!-- inptus -->
              <div class="field">
                <div class="control">
                  <input class="input" type="text" placeholder="اسمك" v-model="firstName" />

                  <input class="input" type="text" placeholder="الرقم السرى" v-model="password" />

                  <button class="button is-primary" @click="submit()">تسجيل الدخول</button>
                </div>
              </div>

              <!-- inptus -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
const usersArray =
  "https://pharmacy-databeas.herokuapp.com/userCustomer-information";
export default {
  data() {
    return {
      password: "",
      firstName: ""
    };
  },
  methods: {
    async submit() {
      localStorage.setItem("userpassword", this.password);
      localStorage.setItem("userfirstName", this.firstName);
      localStorage.setItem("myPharmacyName", this.pharmacyName);
      const nameres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/userCustomer-information/?firstName=${this.firstName}`
      );
      const basswordres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/userCustomer-information/?password=${this.password}`
      );
      console.log(nameres.data, basswordres.data);
      if (nameres.data.length > 0 && basswordres.data.length > 0) {
        this.$router.replace("/drugs");
      } else {
        alert("الرقم السرى  او اسم المستخدم خطأ");
      }
    }
  }
};
</script>

<style  scoped>
.control {
  text-align: center;
}
.signIn {
  position: absolute;
  /* background: #0000009c; */
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
  /* margin-right: 20px; */
  /* margin-top: 20%; */
}

.signIncard {
  flex-basis: calc(50% - 20px);
  display: inline-block;
  background-color: transparent;
  margin: 10px;
  padding: 10px;
  color: #fff;
  text-align: center;
}
.signIncards input {
  margin: 15px 0;
}

.mybuttons button {
  /* margin-right: 35px; */
  width: 250px;
}
.myinputs {
  /* margin-top: 10% !important; */
  background-color: #40407e;
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  padding: 20px 50px;
}
.inputimg {
  width: 100px;
}
.slogan {
  padding: 100px 0;
}

@media screen and (max-width: 768px) {
  .slogan {
    padding: 0;
  }

  .signIn {
    position: absolute;
    /* background: #0000009c; */
    top: 0%;
    bottom: 0;
    right: 0;
    left: 0;
    transform: translate(0, -0%);
  }

  .signIncards {
    margin-right: 0;
  }
  .signIncard {
    flex-basis: calc(100% - 10px);
  }
  .mybuttons button {
    margin-right: 0;
    margin-top: 20px;
  }
}
</style>