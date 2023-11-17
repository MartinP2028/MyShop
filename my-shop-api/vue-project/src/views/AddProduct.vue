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
            "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAyNDc5ODYsImV4cCI6MTcwMDI1MTU4Niwicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6Im1hcnRpbi5waW5hdWRAZXBpdGVjaC5kaWdpdGFsIn0.Zt_tVpgTztUxKw0qyu4ilgWCwa4E41-TgPaGvbH9FmlDVGApyz_6LJuGWXwnNDD7DBybxfSXXCCCqW10Ij3WloVowrmww1kn4PUae_g514b9PEJIxLFOsjsPrpYDSXMVT92x1B1LZdzP7Ag51D5YTQNTJ3Sz3zLJdrbu7bM8fyNI-uOr65iEa8sDQXo9DQeEvRr6OGD3DYgK_kqYCtPos0SJBH6ekPR0-AZxP9Z8j7qPwa8py4sVQNNOTFiYbcC2JDonPMDFTk1m3quNbNsTCcckVCDqYHj4SSo4rZBvchzDPWQ42ZlUXBTiryBS-w7DRGZu-Zs7JytvCfW0TDbrmw",
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          name: this.Name,
          description: this.Description,
          price: parseFloat(this.Price),
          categories: [this.Categories],
        }),
      };
      fetch("http://localhost/api/products", requestOptions).then(
        () => console.log("Product added test"),
        document.location = "http://localhost:5173/",
        location.reload()
      );
    },
  },
};
</script>

<style></style>
