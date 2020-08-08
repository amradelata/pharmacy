<template>
  <div class="signIn">
    <div class="overlay">
      <div class="signIncards">
        <div class="signIncard">
          <!-- <p class="is-size-1 head">صيدلية</p>
          <p class="is-size-3">اول موقع لتوصيل الأدويه فى العالم العربى</p>-->
          <div class="myimg"></div>
        </div>
        <div class="signIncard myquestion">
          <p class="is-size-3 has-text-black">ما نوع الحساب الذى تريد انشائه ؟</p>
          <!--putons  -->
          <div class="mybuttons">
            <button class="button is-medium is-primary" @click="useroner()">مشترى</button>

            <button class="button is-medium is-primary" @click="usercustomer()">مالك صيدلية</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return { userstat: "" };
  },
  methods: {
    usercustomer() {
      this.userstat = "oner";
      this.$router.replace("/signInOner3");
      console.log(this.userstat);
    },
    useroner() {
      this.userstat = "customer";
      this.$router.replace("/signInCustumer3");
      console.log(this.userstat);
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
  /* margin-right: 20px; */
  text-align: center;
  /* margin-top: 20%; */
}

.myimg {
  height: 152%;
  width: 100%;

  background-image: url("https://static.dribbble.com/users/3837152/screenshots/6791073/7.png");
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
}
.myquestion {
  margin-top: 10% !important;
}
.signIncard {
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
  /* margin-right: 35px; */
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