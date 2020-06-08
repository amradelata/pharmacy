<template>
  <div></div>
</template>

<script>
import axios from "axios";
const usersArray = "https://pharmacy-databeas.herokuapp.com/user-information";
export default {
  data() {
    return {
      userstat: localStorage.getItem("userstat"),
      myFirstNmae: localStorage.getItem("userfirstName"),
      myBassword: localStorage.getItem("userpassword")
    };
  },
  async mounted() {
    const nameres = await axios.get(
      `https://pharmacy-databeas.herokuapp.com/user-information/?firstName=${this.myFirstNmae}`
    );
    if (nameres.data.length <= 0) {
      this.$router.replace("/signIn");
    } else if (
      nameres.data.length > 0 &&
      nameres.data[0].userstat === "customer"
    ) {
      this.$router.replace("/customer");
    } else if (nameres.data.length > 0 && nameres.data[0].userstat === "oner") {
      this.$router.replace("/pharmacyowner");
    }
    // console.log(this.$refs["oner"], this.$refs["custumer"]);
    // console.log(nameres.data[0].userstat);
  }
};
</script>
