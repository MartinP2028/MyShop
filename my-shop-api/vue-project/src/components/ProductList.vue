<template>
  <section class="grid-item">
    <img
      src="../../img/white_color.png"
      class="furniture-image"
      alt="Photo canapé lounge"
    />
    <div class="left-part">
      <ul>
        <li class="furniture-name">{{ product.name }}</li>
        <li class="furniture-type">{{ product.description }}</li>
        <li>
          <img
            class="stars"
            src="../../img/four_stars.png"
            alt="Four stars rating"
          />
        </li>
      </ul>
    </div>
    <div class="right-part">
      <ul>
        <li class="price">{{ product.price }} €</li>
        <li>
          <img
            class="plus-item-cart"
            src="../../img/plus_item_cart.png"
            alt="Plus item cart"
          />
        </li>
      </ul>
    </div>
  </section>
</template>

<script setup>
defineProps(["product"]);
</script>
