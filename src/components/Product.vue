<template>
  <b-col xl="2" lg="3" md="3" sm="4" cols="12" class="mb-4">
    <b-card class="mb-4 border-0">
      <b-card-img-lazy :src="product.image" height="200"></b-card-img-lazy>
      <b-card-body>
        <b-card-title
          v-b-modal.modal-center
          @click="$bvModal.show('modal-productDetails-' + product.productId)"
        >{{ product.productName }}</b-card-title>
        <b-card-sub-title class="mb-2">{{ product.price }}€</b-card-sub-title>
      </b-card-body>


      <b-button
        size="sm"
        v-show="product.quantity > 0"
        variant="light"
        class
      >{{ product.quantity }} </b-button>

      <b-button size="sm" v-show="product.quantity === 0" variant="light" @click="addToCart" class>
        <font-awesome-icon icon="shopping-cart" class="mr-1" /> Ajouté au panier
      </b-button>

    </b-card>

    <ProductDetails :ProductDetails="product" />
  </b-col>
</template>

<script>
import { mapState } from "vuex";
import ProductDetails from "@/components/ProductDetails.vue";

export default {
  components: {
    ProductDetails
  },
  props: {
    productPros: {
      type: Object,
      required: true
    }
  },
  data: function() {
    return {
    };
  },
  methods: {
    addToCart() {
      this.$store.dispatch("addToCart", this.product);
    },
    removeFromCart() {
      this.$store.dispatch("removeFromCart", this.product);
    }
  },
  computed: {
    product() {
      const findItem = this.cartItems.find(
        element => element.productId === this.productPros.productId
      );
      if (findItem) {
        return findItem;
      } else {
        return {
          id: this.productPros.productId,
          name: this.productPros.productName,
          price: this.productPros.productPrice,
          image: this.productPros.productPicture,
          description: this.productPros.description,
          quantity: 0
        };
      }
    },
    ...mapState(["cartItems"])
  }
};
</script>

<style lang="scss" scoped>
.card-body {
  padding: 6px 10px 20px 10px;
}
.card-title {
  cursor: pointer;
  font-size: 22px;
}
.card-title:hover {
  color: #007bff;
}
</style>
