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
    const nameCustomerres = await axios.get(
      `https://pharmacy-databeas.herokuapp.com/userCustomer-information/?firstName=${this.myFirstNmae}`
    );
    const nameresOner = await axios.get(
      `https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information/?firstUserName=${this.myFirstNmae}`
    );
    if (nameCustomerres.data.length <= 0 && nameresOner.data.length <= 0) {
      this.$router.replace("/signIn");
    } else if (
      nameCustomerres.data.length > 0 &&
      nameCustomerres.data[0].userstat === "customer"
    ) {
      this.$router.replace("/drugs");
    } else if (
      nameresOner.data.length > 0 &&
      nameresOner.data[0].userstat === "oner"
    ) {
      this.$router.replace("/pharmacyowner");
    }
    // console.log(this.$refs["oner"], this.$refs["custumer"]);
    // console.log(nameres.data[0].userstat);
  }
};
</script>
