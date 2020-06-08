<template>
  <div>
    <myVav />
    <div class="container">
      <div class="setingsuser">
        <div class="head">
          <span class="itemright">الحساب</span>
          <button class="itemleft button is-rounded">حفظ</button>
        </div>
        <div class="suphead">
          <span>بيانات الخصوصية</span>
        </div>
        <div class="item">
          <div class="itemright">الاسم</div>
          <div class="itemleft">{{userInformation.firstName}}</div>
        </div>
        <div class="item">
          <div class="itemright">الرقم الهاتف</div>
          <div class="itemleft">90010</div>
        </div>
        <div class="item">
          <div class="itemright">اسم العائلة</div>
          <div class="itemleft">{{userInformation.lastName}}</div>
        </div>
        <div class="item">
          <div class="itemright">البريد</div>
          <div class="itemleft">{{userInformation.email}}</div>
        </div>
        <div class="item">
          <div class="itemright">نوع الحساب</div>
          <div class="itemleft">{{userInformation.userstat}}</div>
        </div>
        <div class="item">
          <div class="itemright">تعديل كلمة السر</div>
          <div class="itemleft">{{userInformation.password}}</div>
        </div>
        <div style="text-align: center; padding: 100px 20px">
          <button class="button is-light" style="width: 100%" @click="logout()">نسجيل الخروج</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import myVav from "~/components/myVav.vue";
import axios from "axios";
const usersArray = "https://pharmacy-databeas.herokuapp.com/user-information";
export default {
  components: {
    myVav
  },
  data() {
    return {
      myuser: localStorage.getItem("userfirstName"),
      userInformation: []
    };
  },
  methods: {
    logout() {
      window.localStorage.clear();
      this.$router.replace("/logIn");
    }
  },
  async created() {
    const res = await axios.get(
      `https://pharmacy-databeas.herokuapp.com/user-information/?firstName=${this.myuser}`
    );
    this.userInformation = res.data[0];
    console.log(res.data[0]);
    console.log(this.myuser);
  }
};
</script>

<style scoped>
.head {
  padding: 50px 0;
}

.setingsuser {
  color: aliceblue;
  height: 100vh;
}
.itemright,
.itemleft {
  display: inline-block;
}
.item {
  border-bottom: 1px solid #cccccc38;
  position: relative;
  padding: 20px 0;
}
.itemright {
  text-align: start;
}
.itemleft {
  position: absolute;
  left: 0;
}
.suphead {
  background: #e2e2e2;
  padding: 15px;
  color: #000;
}
.itemimg {
  padding: 100px 0;
  padding-top: 30px;
}
@media screen and (max-width: 768px) {
  .itemright {
    padding-right: 20px;
  }

  .itemleft {
    left: 20px;
  }
}
</style>