<template>
  <div>
    <div class="home">
      <div class="hometext">
        <!-- inptus -->
        <div class="field">
          <div class="control">
            <!--acunt tayp  -->
            <div class="control">
              <p class="is-size-1 has-text-black">نوع الحساب</p>
              <button class="button is-large is-primary" @click="useroner()">مشترى</button>
              <span class="mideltext has-text-black">او</span>
              <button class="button is-large is-primary" @click="usercustomer()">مالك صيدلية</button>
            </div>
            <!-- acunt tayp -->
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
.control {
  text-align: center;
}
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