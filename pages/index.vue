<template>
  <div class="container mx-auto">
    <Header />
    <div class="py-4">
      <input
        type="search"
        placeholder="Search products"
        class="px-4 py-2 w-full rounded-full focus:rounded-full border b-gray-100 focus:b-gray-100 outline-none"
      />
    </div>
    <div class="py-4">
      <div class="">
        Product
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, $config: { consumerKey, consumerSecret } }) {
    const prods = await $axios.$get(
      `/products?consumer_key=${consumerKey}&consumer_secret=${consumerSecret}`
    );
    console.log(prods);
  }
};
</script>
