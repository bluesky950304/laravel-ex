<template>
  <section class="text-gray-700 body-font overflow-hidden" v-if="v_product">
    <div class="container px-12 py-24 mx-auto">
      <div class="lg:w-3/5 mx-auto flex flex-wrap">
        <img
          alt="ecommerce"
          class="lg:w-1/2 w-full lg:h-auto h-64 object-cover object-center rounded"
          src="https://dummyimage.com/640x640"
        />
        <div class="lg:w-1/2 w-full lg:pl-10 lg:py-6 mt-6 lg:mt-0">
          <h2
            class="text-sm title-font text-gray-500 tracking-widest uppercase inline-block mr-2"
            v-for="item_category in v_product.categories"
            v-text="item_category.name"
            :key="item_category.id"
          ></h2>
          <h1
            class="text-gray-900 text-3xl title-font font-medium mb-2"
            v-text="v_product.name"
          ></h1>
          <p class="leading-relaxed" v-text="v_product.description"></p>
          <div class="flex mt-6 pt-4 border-t-2 border-gray-200">
            <span
              class="title-font font-medium text-2xl text-gray-900"
              v-text="onFormatCurrency(v_product.price)"
            ></span>
            <button
              class="flex ml-auto text-white bg-indigo-500 border-0 py-2 px-6 focus:outline-none hover:bg-indigo-600 rounded"
              @click="$store.commit('addToCart', v_product)"
            >
              Add To Cart
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  methods: {
    onFormatCurrency(amount) {
      amount = amount / 100;
      return amount.toLocaleString(process.env.MIX_CASHIER_CURRENCY_LOCALE, {
        style: "currency",
        currency: process.env.MIX_CASHIER_CURRENCY,
      });
    },
  },
  computed: {
    v_products() {
      return this.$store.state.state_products;
    },
    v_product() {
      return this.v_products.find(
        (product) => product.slug === this.$route.params.slug
      );
    },
  },
};
</script>