<template>
  <div class="user">
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
          <div class="itemleft">{{pharmsyInformation.firstUserName}}</div>
        </div>
        <div class="item">
          <div class="itemright">اسم الصيدلية</div>
          <div class="itemleft">{{pharmsyInformation.pharmacyName}}</div>
        </div>

        <div class="item">
          <div @click="showeditLastname()" class="items">
            <div class="itemright">الرقم الهاتف</div>
            <div class="itemleft">{{pharmsyInformation.userphone}}</div>
          </div>

          <div class="edit" ref="lastnameedit">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="pharmsyInformation.userphone"
              ref="userphoneinput"
            />
          </div>
        </div>

        <div class="item">
          <div @click="showeditEmail ()" class="items">
            <div class="itemright">البريد</div>
            <div class="itemleft">{{pharmsyInformation.email}}</div>
          </div>

          <div class="edit" ref="edit">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="pharmsyInformation.email"
              ref="emailinput"
            />
          </div>
        </div>
        <div class="item">
          <div class="itemright">نوع الحساب</div>
          <div class="itemleft">{{pharmsyInformation.userstat}}</div>
        </div>

        <div class="item">
          <div @click="showeditpassword()" class="items">
            <div class="itemright">تعديل كلمة السر</div>
            <div class="itemleft">{{pharmsyInformation.password}}</div>
          </div>

          <div class="edit" ref="editPassword">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="pharmsyInformation.password"
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
const useronerpharmsy =
  "https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information";
export default {
  components: {
    myVav
  },
  data() {
    return {
      userName: localStorage.getItem("userfirstName"),
      pharmsyInformation: []
    };
  },
  methods: {
    async seave() {
      const emailinputvalue = this.$refs["emailinput"].value;
      const userphoneinput = this.$refs["userphoneinput"].value;
      const passwordinput = this.$refs["passwordinput"].value;
      let id = this.pharmsyInformation.id;
      console.log(id);

      const res = await axios.patch(
        `https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information/${id}`,
        {
          email: emailinputvalue,
          password: passwordinput,
          userphone: userphoneinput
        }
      );
      this.$router.go();
      const edi = await axios.get(useronerpharmsy);
      this.userInformation = edi.data;
    },
    logout() {
      localStorage.setItem("userpassword", null);
      localStorage.setItem("userfirstName", null);
      localStorage.setItem("myPharmacyName", null);
      this.$router.replace("/");
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
    const ressearch = await axios.get(
      `https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information/?firstUserName=${this.userName}`
    );
    console.log(ressearch.data[0]);
    this.pharmsyInformation = ressearch.data[0];
  }
};
</script>

<style scoped>
.user {
  background: #1d2c4d;
}
.asd {
  text-align: left;
  margin-top: 10px;
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