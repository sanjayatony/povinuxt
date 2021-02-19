<template>
  <div class="container mx-auto">
    <Header />
    <div class="py-4">
      <form method="GET" action="#" @submit.prevent="search">
        <input
          type="search"
          v-model="searchProduct"
          placeholder="Search products"
          class="px-4 py-2 w-full rounded-full focus:rounded-full border b-gray-100 focus:b-gray-100 outline-none"
        />
      </form>
    </div>
    <div
      class="py-4 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-x-16 gap-y-16"
    >
      <article
        class="text-center"
        v-for="product in products"
        :key="product.id"
      >
        <img :src="product.images[0].src" />
        <h2 class="font-bold text-xl">{{ product.name }}</h2>
        <div>{{ product.price }}</div>
      </article>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchProduct: "",
      products: ""
    };
  },
  async asyncData({ $axios, $config: { consumerKey, consumerSecret } }) {
    const products = await $axios.$get(
      `/products?consumer_key=${consumerKey}&consumer_secret=${consumerSecret}`
    );
    return { products };
  },
  methods: {
    async search() {
      const prods = await this.$axios.$get(
        `/products?search=${this.searchProduct}&consumer_key=ck_1c5b1500672a9d4a0596d79936c5e9db2606c3a8&consumer_secret=cs_fd50e35416c818025966451e0bcf7dec49b61625`
      );
      this.products = prods;
    }
  }
};
</script>
