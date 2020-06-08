<template>
  <div>
    <myVav />
    <div class="container">
      <div class="setingsuser">
        <div class="head">
          <span class="itemright">الحساب</span>
          <button class="itemleft button is-rounded" @click="seave()">حفظ</button>
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
          <div @click="showeditLastname()" class="items">
            <div class="itemright">اسم العائلة</div>
            <div class="itemleft">{{userInformation.lastName}}</div>
          </div>

          <div class="edit" ref="lastnameedit">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="userInformation.lastName"
              ref="lastnameemailinput"
            />
          </div>
        </div>

        <div class="item">
          <div @click="showeditEmail ()" class="items">
            <div class="itemright">البريد</div>
            <div class="itemleft">{{userInformation.email}}</div>
          </div>

          <div class="edit" ref="edit">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="userInformation.email"
              ref="emailinput"
            />
          </div>
        </div>
        <div class="item">
          <div class="itemright">نوع الحساب</div>
          <div class="itemleft">{{userInformation.userstat}}</div>
        </div>

        <div class="item">
          <div @click="showeditpassword()" class="items">
            <div class="itemright">تعديل كلمة السر</div>
            <div class="itemleft">{{userInformation.password}}</div>
          </div>

          <div class="edit" ref="editPassword">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="userInformation.password"
              ref="passwordinput"
            />
          </div>
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
    async seave() {
      const emailinputvalue = this.$refs["emailinput"].value;
      const lastnameemailinput = this.$refs["lastnameemailinput"].value;
      const passwordinput = this.$refs["passwordinput"].value;
      let id = this.userInformation.id;
      console.log(id);

      const res = await axios.patch(
        `https://pharmacy-databeas.herokuapp.com/user-information/${id}`,
        {
          email: emailinputvalue,
          lastName: lastnameemailinput,
          password: passwordinput
        }
      );
      this.$router.go();
      const edi = await axios.get(usersArray);
      this.userInformation = edi.data;
    },
    logout() {
      window.localStorage.clear();
      this.$router.replace("/logIn");
    },
    showeditEmail() {
      this.$refs["edit"].classList.toggle("edit");
    },
    showeditLastname() {
      this.$refs["lastnameedit"].classList.toggle("edit");
    },
    showeditpassword() {
      this.$refs["editPassword"].classList.toggle("edit");
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
.asd {
  text-align: left;
}
.edit {
  display: none;
  padding: 20px 0;
}
.items {
  cursor: pointer;
  user-select: none;
}
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