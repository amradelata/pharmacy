
<script>
export default {
  data() {
    return {
      userstat: localStorage.getItem("userstat")
    };
  },
  mounted() {
    if (this.userstat === null) {
      this.$router.replace("/signIn");
    } else if (this.userstat === "customer") {
      this.$router.replace("/customer");
    } else if (this.userstat === "oner") {
      this.$router.replace("/pharmacyowner");
    }
    console.log(this.$refs["oner"], this.$refs["custumer"]);
  }
};
</script>
