<template>
  <div class="home">
    <b-container fluid>
      <b-row>
        <div class="col-lg-12 mt-4">
          <div class="row">
            <product v-for="product in products" :key="product.id" :productPros="product" />
          </div>
        </div>
      </b-row>
      <div class="row mb-5">
        
      </div>
    </b-container>
  </div>
</template>

<script>
// @ is an alias to /src
import Product from "@/components/Product.vue";
import { mapState } from "vuex";

export default {
  name: "home",
  components: { Product },
  
  methods: {},
  created() {
    this.perPage = 12;
    this.$store.dispatch("getProducts", {
      perPage: this.perPage,
      page: this.page
    });
  },
  computed: {
    page() {
      return parseInt(this.$route.query.page) || 1;
    },
    hasNextPage() {
      return this.totalProducts > this.page * this.perPage;
    },
    ...mapState(["products", "totalProducts"])
  }
};
</script>
