<template>
  <div class="signIn">
    <div class="overlay">
      <div class="signIncards">
        <div class="signIncard">
          <p class="is-size-1 head">صيدلية</p>
          <p class="is-size-3 has-text-black">اول موقع لتوصيل الأدويه فى العالم العربى</p>
        </div>
        <div class="signIncard">
          <div class="myinputs">
            <p class="is-size-3 has-text-black">حساب مشترى</p>
            <!--putons  -->
            <div class="mybuttons">
              <!-- inptus -->
              <div class="field">
                <div class="control">
                  <input class="input is-primary" type="text" placeholder="الاسم" v-model="name" />
                  <input class="input is-primary" type="text" placeholder="الايميل" v-model="email" />

                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="الرقم السرى"
                    v-model="password"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="رقم الهاتف"
                    v-model="userphone"
                  />

                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="حطوط العرض- موقعك"
                    v-model="pharmacyLatitude"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="خطوط الطول- موقعك"
                    v-model="pharmacyLongitude"
                  />

                  <button class="button is-primary" @click="submit()">تسجيل الحساب</button>
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
      userphone: "",
      password: "",
      email: "",
      name: "",
      pharmacyLongitude: "",
      pharmacyLatitude: ""
    };
  },
  methods: {
    async submit() {
      const nameres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/userCustomer-information/?firstName=${this.name}`
      );
      if (nameres.data.length > 0) {
        alert("هذا الاسم موجود بالفعل ");
        return;
      } else if (
        this.firstName === "" ||
        this.email === "" ||
        this.password === "" ||
        this.userphone === "" ||
        this.Latitude === "" ||
        this.Longitude === ""
      ) {
        alert("من فضلك فم بمليء كل البيانات ");
        return;
      } else {
        const res = await axios.post(usersArray, {
          firstName: this.name,
          email: this.email,
          password: this.password,
          userphone: this.userphone,
          userstat: "customer",
          Latitude: this.pharmacyLatitude,
          Longitude: this.pharmacyLongitude
        });
      }

      // localStorage.setItem("userstat", "customer");
      localStorage.setItem("userfirstName", this.name);
      //   localStorage.setItem("userfirstName", this.firstName);
      //   localStorage.setItem("userlastName", this.lastName);
      //   localStorage.setItem("useremail", this.email);
      //   localStorage.setItem("userpassword", this.password);
      //   localStorage.setItem("userstat", this.userstat);
      this.$router.replace("/customer");
      // const useracount = localStorage.getItem("userstat");
      // if (useracount == "customer") {
      // } else if (useracount == "oner") {
      //   this.$router.replace("/pharmacyowner");
      // }
    }
  }
};
</script>

<style  scoped>
.signIn {
  /* background-image: url("https://image.freepik.com/free-vector/abstract-health-medical-science-healthcare-icon_36402-276.jpg") !important; */
  background-position: center center;
  background-size: cover;
  text-align: center;
  position: relative;
  height: 100vh;
  width: 100vw;
  overflow-x: hidden;
  overflow-y: hidden;
}
.overlay {
  position: absolute;
  /* background: #0000009c; */
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
}
.head {
  color: #00d1b2;
}
.signIncards {
  display: flex;
  flex-wrap: wrap;
  margin-right: 20px;
  margin-top: 20%;
}

.signIncard {
  flex-basis: calc(50% - 20px);
  display: inline-block;
  background-color: transparent;
  margin: 10px;
  padding: 10px;
  color: #fff;
}
.signIncards input {
  margin: 5px 0;
  /* width: 250px; */
}

.mybuttons button {
  margin-right: 35px;
}
.myinputs {
  margin-top: -100px;
}
.control {
  text-align: center;
}
@media screen and (max-width: 768px) {
  .signIn {
    height: 150vh;
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
  .myinputs {
    margin-top: 0;
  }
}
</style>