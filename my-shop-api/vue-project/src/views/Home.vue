<template>
  <main class="home">
    <div
      class="grid-container"
      v-if="getProducts.data && getProducts.data['hydra:member']"
    >
      <section class="grid-item">
        <p class="filter-by">FILTER BY</p>
        <ul class="filtrebar">
          <li class="filter">Collection</li>
          <img class="arrow" src="img/fleche.svg" alt="fleche" />
        </ul>
        <ul class="filtrebar">
          <li class="filter">Color</li>
          <img class="arrow" src="img/fleche.svg" alt="fleche" />
        </ul>
        <ul class="filtrebar">
          <li class="filter">Category</li>
          <img class="arrow" src="img/fleche.svg" alt="fleche" />
        </ul>
        <p class="filter">Price Range</p>
        <div class="pricebar">
          <div class="price_range">
            <div class="range-slider">
              <input
                type="range"
                class="min-price"
                value="0"
                min="0"
                max="10000"
                step="1"
              />
              <input
                type="range"
                class="max-price"
                value="10000"
                min="0"
                max="10000"
                step="1"
              />
            </div>
            <div class="price-content">
              <p class="price" id="min-value">$0</p>
              <p class="price" id="max-value">$10,000+</p>
            </div>
          </div>
        </div>
      </section>
      <ProductList
        class="grid-item"
        v-for="product in getProducts.data['hydra:member']"
        :product="product"
      />
    </div>
  </main>
</template>

<script>
// Importation des actions et des états du store "products"
import { useProducts } from "../stores/counter.js";
import { mapActions, mapState } from "pinia";
import ProductList from "../components/ProductList.vue";

export default {
  components: {
    ProductList,
  },
  data() {
    return {
      // Initialisation de l'état local "products"
      products: [],
    };
  },
  async mounted() {
    // Récupération des produits depuis l'API lors du montage du composant
    await this.fetchProduct;
  },
  computed: {
    // Mappage des actions du store "products"
    ...mapActions(useProducts, ["fetchProduct"]),
    // Mappage des états du store "products"
    ...mapState(useProducts, ["getProducts"]),
  },
  methods: {},
};
</script>

<style>
body {
  color: black;
}
</style>
