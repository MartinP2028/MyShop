<template>
  <p>{{ getProducts.data["hydra:member"] }}</p>
  <RouterView />
</template>

<script>
// Importation des actions et des états du store "products"
import { useProducts } from "../stores/counter.js";
import { mapActions, mapState } from "pinia";

export default {
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
  color: white;
}
</style>
