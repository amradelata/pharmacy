<template>
  <div class="home">
    <div class="hometext">
      <p class="is-size-1">هل انت</p>
      <div class="button is-large is-primary" to="/pharmacyowner" @click="useroner()">مالك صيدلية</div>
      <span class="mideltext">او</span>
      <div class="button is-large is-primary" @click="usercustomer()">مشترى</div>
    </div>
  </div>
</template>
<script>
import notification from "~/components/notification.vue";

export default {
  components: {
    notification
  },
  methods: {
    youHaveOrder() {
      this.$refs["newOrder"].classList.toggle("displayNone");
    },
    usercustomer() {
      localStorage.setItem("userstat", "customer");
      this.$router.replace("/customer");
    },
    useroner() {
      localStorage.setItem("userstat", "oner");
      this.$router.replace("/pharmacyowner");
    }
  }
};
</script>

<style scoped>
.home {
  text-align: center;
  position: relative;
  height: 100vh;
  width: 100vw;
}
.home p {
  margin-bottom: 100px;
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
@media screen and (max-width: 768px) {
  .mideltext {
    display: block;
    margin: 35px;
  }
}
</style>