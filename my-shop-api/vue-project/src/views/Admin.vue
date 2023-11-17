<template>
  <section class="admin">
    <div
      class="grid-container"
      v-if="getProducts.data && getProducts.data['hydra:member']"
    >
      <div class="titles">
        <h1>
          <button class="title">Products
          </button>
        </h1>
        <h1>
          <button class="title">Categories</button>
        </h1>
        <h1>
          <button class="title">Users</button>
        </h1>
        <h1>
          <button @click="addItem" class="add">Add New</button>
        </h1>
      </div>
      <div class="product-grid">
        <div class="product-grid-name">
          <p class="cat">Name</p>
          <p class="cat">Description</p>
          <p class="cat">Price</p>
          <p class="cat">Id</p>
          <p class="cat">Categories</p>
          <p class="cat">Actions</p>
        </div>
        <article
          v-for="product in getProducts.data['hydra:member']"
          :key="product.id"
          class="colonne"
        >
          <p class="col">{{ product.name }}</p>
          <p class="col">{{ product.description }}</p>
          <p class="col">{{ product.price }}</p>
          <p class="col">{{ product.id }}</p>
          <p class="col">{{ product.categories }}</p>
          <button class="col" @click="editItem(product.id)">Edit</button>
          <button class="col" @click="deleteItem(product.id)">Delete</button>
        </article>
      </div>
    </div>
  </section>
</template>

<script>
import { useProducts } from "../stores/counter.js";
import { mapActions, mapState } from "pinia";

export default {
  data() {
    return {
      // products: [],
      showProducts: true, // Default to show products
      showCategories: false,
      showUsers: false,
    };
  },
  async mounted() {
    this.products = await this.fetchProduct;
  },
  computed: {
    ...mapActions(useProducts, ["fetchProduct"]),
    ...mapState(useProducts, ["getProducts"]),
  },
  methods: {
    deleteItem(id) {
      const requestOptions = {
        method: "DELETE",
        headers: {
          Authorization:
            "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyMzA5NjgsImV4cCI6MTcwMDIzNDU2OCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6Im1hcnRpbi5waW5hdWRAZXBpdGVjaC5kaWdpdGFsIn0.l3j7BwoeB0lGXm4BMHR8orZEMRmVK-rKr2CzJkr6ASmibWnk2HH2OdMv0Tb2phF1FfgpHpRRHLJvWCalBNFcOGlKJEwOhT65Se0OlXeWXit27CY38aDLkPVpFG6yOwUKyfnLqcrGPMGS4lSQ9zdB_RXkwEbURK1-Z5gkfIJblG8FKq318aNQMdZn5PWslzOMXWwK2jjP_MPOR-mq-fs6SRJfEWlx384SIGXjAhOTpi4PfQfpRAQyOR9uzRHdTioTbwsJBKrmDByfJ-qFrRkUilfxlYxACYMC8wEVzFUTjLxHXSC1ah-D0cX4llrOymdiJhSM4FU4NTkV2XtZv95-3A",
          "Content-Type": "application/json",
        },
      };
      fetch("http://localhost/api/products/" + id, requestOptions).then(
        () => this.products
      );
    },
    addItem() {
      document.location = "/addproduct";
    },
  },
};
</script>

<style scoped>
.admin {
  height: 35vw;
}
.titles {
  display: flex;
  justify-content: center;
  gap: 20px;
}
.product-grid {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.product-grid-name {
  display: flex;
  gap: 150px;
}

.colonne {
  display: flex;
  justify-content: space-between;
  border-top: 1px solid #ccc;
  padding-top: 20px;
}
</style>
