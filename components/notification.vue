<template>
  <div>
    <div class="btncontaner">
      <button
        ref="cangemybtn"
        @click="togelnotification()"
        class="button is-medium is-fullwidth mybtn"
      >متصل</button>
    </div>

    <div class="notification borderRadus is-primary" ref="primary">انت الان تسطاتيع استقبال الطلبات</div>
    <div
      class="notification borderRadus is-danger displayNone"
      ref="danger"
    >انت غير متصل لن تتمكن من استقبال الطلبات</div>
  </div>
</template>
<script>
export default {
  methods: {
    togelnotification() {
      this.$refs["primary"].classList.toggle("displayNone");
      this.$refs["danger"].classList.toggle("displayNone");
      let herobtn = this.$refs["cangemybtn"];

      if (herobtn.innerHTML === "متصل") {
        herobtn.innerHTML = "غير متصل";
        herobtn.style.background = "#9297b8";
      } else {
        herobtn.innerHTML = "متصل";
        herobtn.style.background = "#2cd1b2";
      }
    }
  }
};
</script>
<style scoped>
.borderRadus {
  border-radius: 0 !important;
}
</style>