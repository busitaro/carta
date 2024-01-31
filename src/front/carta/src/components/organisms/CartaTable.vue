<template>
  <div class="block w-11/12 h-screen mx-auto bg-blue-100">
    <CartaCard />
    <slot></slot>
  </div>
</template>

<script>
import CartaCard from "~/components/organisms/CartaCard.vue";

export default {
  components: {
    CartaCard,
  },
};
</script>
