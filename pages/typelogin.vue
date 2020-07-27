<template>
  <div class="signIn">
    <div class="overlay">
      <div class="signIncards">
        <div class="signIncard">
          <p class="is-size-1 head">صيدلية</p>
          <p class="is-size-3">اول موقع لتوصيل الأدويه فى العالم العربى</p>
        </div>
        <div class="signIncard">
          <p class="is-size-3">ما نوع حسابك ؟</p>
          <!--putons  -->
          <div class="mybuttons">
            <button class="button is-primary is-medium" @click="useroner()">مشترى</button>

            <button class="button is-primary is-medium" @click="usercustomer()">مالك صيدلية</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    usercustomer() {
      this.userstat = "oner";
      this.$router.replace("/loginoner3");
      console.log(this.userstat);
    },
    useroner() {
      this.userstat = "customer";
      this.$router.replace("/logincustmer3");
      console.log(this.userstat);
    }
  }
};
</script>


<style  scoped>
.signIn {
  background-image: url("https://image.freepik.com/free-vector/abstract-health-medical-science-consist-dna_36402-305.jpg") !important;
  background-position: center center;
  background-size: cover;
  text-align: center;
  position: relative;
  height: 100vh;
  width: 100vw;
}
.overlay {
  position: absolute;
  background: #0000009c;
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
}
</style>