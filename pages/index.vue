<template>
  <div class="container">
    <div v-for="product in products" :key="product._id">
      <div class="title">
        <h3>{{ product.title }}</h3>
        <p>{{ product.blurb }}</p>
      </div>

      <div class="content">
        <div class="BOX">
          <div class="pic">
            <img :src="product.imageUrl" alt="" />
          </div>
        </div>
      </div>

      <div class="more">
        <nuxt-link :to="product.slug.current">
          <p>Learn more</p>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $sanity }) {
    const query = `*[_type == "product"]{
     title,
     slug,
     _id,
     'price': defaultProductVariant.price,
     'imageUrl': defaultProductVariant.images[0].asset->url,
      'blurb': blurb.en
     }`;

    const products = await $sanity.fetch(query);

    return { products };
  }
};
</script>

<style></style>
