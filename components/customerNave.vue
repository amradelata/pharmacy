<template>
  <div class="container is-fluid">
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
          <nuxt-link to="/" class="navbar-item">
            <img src="~/assets/img/home.svg" class="menuImg" />
            الرئيسية
          </nuxt-link>

          <nuxt-link to="/bell" class="navbar-item">
            <img src="~/assets/img/bell.svg" class="menuImg" />
            الاشعارات
          </nuxt-link>

          <nuxt-link to="/user" class="navbar-item">
            <img src="~/assets/img/user.svg" class="menuImg" />
            الحساب
          </nuxt-link>

          <nuxt-link to="/setings" class="navbar-item">
            <img src="~/assets/img/setings.svg" class="menuImg" />
            اعدادات الحساب
          </nuxt-link>

          <nuxt-link to="/help" class="navbar-item">
            <img src="~/assets/img/help.svg" class="menuImg" />
            المساعده
          </nuxt-link>

          <nuxt-link to="/orders" class="navbar-item">
            <img src="~/assets/img/logout.svg" class="menuImg" />
            تسجيل الخروج
          </nuxt-link>
        </div>
      </div>
    </nav>

    <div id="navbarphone" class="navbar-menu" ref="phonemenu">
      <div class="navbar-start">
        <nuxt-link to="/" class="navbar-item">
          <img src="~/assets/img/home.svg" class="menuImg" />
          الرئيسية
        </nuxt-link>

        <nuxt-link to="/orders" class="navbar-item">
          <img src="~/assets/img/orders.svg" class="menuImg" />
          الطلبات
        </nuxt-link>

        <nuxt-link to="/Profits" class="navbar-item">
          <img src="~/assets/img/Profits.svg" class="menuImg" />
          المبيعات و الارباح
        </nuxt-link>

        <nuxt-link to="/bell" class="navbar-item">
          <img src="~/assets/img/bell.svg" class="menuImg" />
          الاشعارات
        </nuxt-link>

        <nuxt-link to="/user" class="navbar-item">
          <img src="~/assets/img/user.svg" class="menuImg" />
          الحساب
        </nuxt-link>

        <nuxt-link to="/setings" class="navbar-item">
          <img src="~/assets/img/setings.svg" class="menuImg" />
          اعدادات الصيدليه
        </nuxt-link>

        <nuxt-link to="/help" class="navbar-item">
          <img src="~/assets/img/help.svg" class="menuImg" />
          المساعده
        </nuxt-link>

        <nuxt-link to="/" class="navbar-item">
          <img src="~/assets/img/logout.svg" class="menuImg" />
          تسجيل الخروج
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    togelmenu() {
      this.$refs["phonemenu"].classList.toggle("navbar-menu");
    }
  }
};
</script>
<style>
.navbar-burger {
  margin-right: auto;
  margin-left: 0;
}
.container.is-fluid {
  padding: 0;
}
.navbar,
#navbarphone {
  padding-right: 35px;
  padding-left: 35px;
  background: #ffffff;
}
</style>
