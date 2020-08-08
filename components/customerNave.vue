<template>
  <div class="is-fluid">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <nuxt-link to="/" class="navbar-item">
          <div class="is-size-3">صيدلية</div>
        </nuxt-link>

        <a
          role="button"
          class="navbar-burger burger"
          aria-label="menu"
          aria-expanded="false"
          data-target="navbarBasicExample"
          @click="togelmenu"
        >
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div id="navbarBasicExample" class="navbar-menu">
        <div class="navbar-start">
          <input
            class="input myinput"
            type="text"
            placeholder="search"
            v-model="searchVale"
            @keyup.enter="searchRout"
          />
          <nuxt-link to="/" class="navbar-item">
            <img src="~/assets/img/home.svg" class="menuImg" />
            الرئيسية
          </nuxt-link>

          <!-- <nuxt-link to="/notificationsCustemer" class="navbar-item">
            <img src="~/assets/img/bell.svg" class="menuImg" />
            الاشعارات
          </nuxt-link>-->

          <nuxt-link to="/userCustomer" class="navbar-item">
            <img src="~/assets/img/user.svg" class="menuImg" />
            الحساب
          </nuxt-link>

          <nuxt-link to="/cart" class="navbar-item cartnav">
            <img src="~/assets/img/cart.png" class="menuImg" />
            <span v-if="this.mylocalStorageQty != 0 " class="cartQty">{{this.mylocalStorageQty}}</span> سلة المشتريات
          </nuxt-link>
          <!-- cart -->
          <div class="mycart">
            <ul class="carts" v-if="this.mylocalStorageCard != null" ref="carts">
              <p class="is-size-3">cart item/s {{this.mylocalStorageQty}}</p>

              <li class="cart" v-for="item in mylocalStorageCard" :key="item.id">
                <div>
                  <p class="is-size-6">{{' name : ' + item.tradename}}</p>
                  <p class="is-size-6 has-text-success">{{ "price : "+item.price + ' EGP'}}</p>
                  {{"qty : "+item.quantity}}
                </div>
              </li>

              <p
                class="is-size-3 has-text-success"
              >{{' Total price : ' + this.mylocalStorageTolalPrice + " EGP"}}</p>

              <nuxt-link to="/checkout">
                <button class="button">Check Out</button>
              </nuxt-link>
              <nuxt-link to="/cart">
                <button class="button">Cart</button>
              </nuxt-link>
            </ul>
          </div>
          <!-- cart -->
          <nuxt-link to="/logoutcustumer" class="navbar-item">
            <img src="~/assets/img/logout.svg" class="menuImg" />
            تسجيل الخروج
          </nuxt-link>
        </div>
      </div>
    </nav>

    <div id="navbarphone" class="navbar-menu" ref="phonemenu">
      <div class="navbar-start">
        <input class="input" type="text" placeholder="search" v-model="searchVale" />
        <button class="searchbtn button" @click="searchRout()">search</button>
        <!--  -->
        <nuxt-link to="/" class="navbar-item">
          <img src="~/assets/img/home.svg" class="menuImg" />
          الرئيسية
        </nuxt-link>

        <!-- <nuxt-link to="/orders" class="navbar-item">
          <img src="~/assets/img/orders.svg" class="menuImg" />
          الطلبات
        </nuxt-link>-->

        <!-- <nuxt-link to="/Profits" class="navbar-item">
          <img src="~/assets/img/Profits.svg" class="menuImg" />
          المبيعات و الارباح
        </nuxt-link>-->

        <!-- <nuxt-link to="/notificationsCustemer" class="navbar-item">
          <img src="~/assets/img/bell.svg" class="menuImg" />
          الاشعارات
        </nuxt-link>-->

        <nuxt-link to="/userCustomer" class="navbar-item">
          <img src="~/assets/img/user.svg" class="menuImg" />
          الحساب
        </nuxt-link>
        <nuxt-link to="/cart" class="navbar-item">
          <img src="~/assets/img/cart.png" class="menuImg" />
          <span class="cartQty">{{this.mylocalStorageQty}}</span> سلة المشتريات
        </nuxt-link>

        <nuxt-link to="/logoutcustumer" class="navbar-item">
          <img src="~/assets/img/logout.svg" class="menuImg" />
          تسجيل الخروج
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchVale: "",
      mylocalStorageCard: [],
      mylocalStorageQty: 0,
      mylocalStorageTolalPrice: 0
      // navcount: false
    };
  },
  methods: {
    togelmenu() {
      this.$refs["phonemenu"].classList.toggle("navbar-menu");
    },
    //pass this.searchVale to link and in search component
    searchRout() {
      this.$router.push("/search?test=" + this.searchVale);
      // this.searchVale = "";
      // window.location.reload(true); ////to relod the page in js and Firefox
      // this.$router.go(); //to relod the page in vue
    }
  },

  mounted() {
    //when i refresh  git my cart data from localStorage
    this.mylocalStorageCard = JSON.parse(localStorage.getItem("cart"));
    this.mylocalStorageTolalPrice = localStorage.getItem("totalprice");
    this.mylocalStorageQty = localStorage.getItem("qty");
  }
};
</script>
<style>
.myinput {
  margin-top: 15px;
}
.searchbtn {
  display: block;
  margin: 10px auto;
}
.cartQty {
  position: absolute;
  height: 17px;
  width: 17px;
  border-radius: 50%;
  text-align: center;
  line-height: 17px;
  color: #fff;
  font-size: 12px;
  top: 8px;
  right: 5px;
  background: #ff424e;
  color: #fff;
}
.cartnav:hover ~ .mycart {
  display: inline-block;
}
.mycart {
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
  padding: 20px;
  position: absolute;
  z-index: 99999;
  background: #ffffff;
  top: 60px;
  left: 60px;
  display: none;
  direction: ltr;
}
.mycart:hover {
  display: inline-block;
}
.navbar-burger {
  margin-right: auto;
  margin-left: 0;
}

.navbar,
#navbarphone {
  padding-right: 35px;
  padding-left: 35px;
  background: #ffffff;
}
</style>
