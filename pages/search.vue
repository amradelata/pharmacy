<template>
  <div>
    <customerNave />
    <div class="mycontainer">
      <ul class="cards">
        <li class="card" v-for="item in drugsSearch" :key="item.id">
          <nuxt-link :to="'/drugs/' + item.id">
            <p class="is-size-4">{{item.tradename}}</p>
            <p class="is-size-6 has-text-primary">{{"price : "+item.price + ' EGP'}}</p>
          </nuxt-link>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import customerNave from "~/components/customerNave.vue";
import axios from "axios";
const API = "https://pharmacy-databeas.herokuapp.com/drugs";
export default {
  components: { customerNave },
  props: [],
  data() {
    return {
      drugsSearch: []
    };
  },
  async created() {
    this.search();
  },
  watch: {
    // test(to, from) {
    //   this.search();
    // }
    "$route.query": {
      immediate: true,
      handler() {
        this.search();
      }
    }
  },
  methods: {
    async search() {
      const res = await axios.get(
        API + "/" + "?tradename_like=" + this.$route.query.test
      );
      this.drugsSearch = res.data;
    }
  }
};
</script>


<style scoped>
.mycontainer {
  width: 100vw;
  padding: 35px 100px;
}
.cards {
  display: flex;
  flex-wrap: wrap;
  /* padding: 0 35px; */
  /* width: 100% */
}
.card {
  flex-basis: calc(33.333% - 20px);
  display: inline-block;
  margin: 10px;
  overflow: hidden;
  padding: 20px;
  text-align: center;
}
@media screen and (max-width: 768px) {
  .card {
    flex-basis: calc(100% - 20px);
  }
  .mycontainer {
    padding: 35px 10px;
  }
}
</style>