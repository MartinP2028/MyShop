<template>
  <section>
    <p>Name</p>
    <input v-model="Name" type="text" />
    <p>Description</p>
    <input v-model="Description" type="text" />
    <p>Price</p>
    <input v-model="Price" type="text" />
    <p>Categories</p>
    <input v-model="Categories" type="text" />
    <button @click="add">Submit Product</button>
  </section>
</template>

<script>
export default {
  data() {
    return {
      Name: "",
      Description: "",
      Price: "",
      Categories: "",
    };
  },
  methods: {
    async add() {
      const requestOptions = {
        method: "POST",
        headers: {
          Authorization:
            "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyMzA5NjgsImV4cCI6MTcwMDIzNDU2OCwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6Im1hcnRpbi5waW5hdWRAZXBpdGVjaC5kaWdpdGFsIn0.l3j7BwoeB0lGXm4BMHR8orZEMRmVK-rKr2CzJkr6ASmibWnk2HH2OdMv0Tb2phF1FfgpHpRRHLJvWCalBNFcOGlKJEwOhT65Se0OlXeWXit27CY38aDLkPVpFG6yOwUKyfnLqcrGPMGS4lSQ9zdB_RXkwEbURK1-Z5gkfIJblG8FKq318aNQMdZn5PWslzOMXWwK2jjP_MPOR-mq-fs6SRJfEWlx384SIGXjAhOTpi4PfQfpRAQyOR9uzRHdTioTbwsJBKrmDByfJ-qFrRkUilfxlYxACYMC8wEVzFUTjLxHXSC1ah-D0cX4llrOymdiJhSM4FU4NTkV2XtZv95-3A",
          "Content-Type": "application/json",
          },
          body: JSON.stringify({
              name: this.Name,
              description: this.Description,
              price: parseFloat(this.Price),
              categories: [this.Categories],
        })
      };
      fetch("http://localhost/api/products", requestOptions).then(
        () => console.log("Product added test")
      );
    },
  },
};
</script>

<style>
</style>
