<template>
  <div class="container">
    <div class="card">
      <div>
        <img :src="product.imageUrl" alt="Product image" style="width:100%" />
      </div>
      <div class="details">
        <h1>{{ product.title }}</h1>
        <div class="price">
          <h3>${{ product.price }}</h3>
        </div>
        <div class="quantity">
          <h3>QUANTITY</h3>
          <input type="number" name="items" id="counter" min="1" value="1" />
        </div>
        <div class="buttons">
          <button>ADD TO CART</button>
          <button>BUY NOW</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ params, $sanity }) {
    const query = `*[_type == "product" && slug.current == "${params.slug}"][0]{
     title,
     slug,
     _id,
     'price': defaultProductVariant.price,
     'imageUrl': defaultProductVariant.images[0].asset->url,
      'blurb': blurb.en
     }`;

    const product = await $sanity.fetch(query);

    return { product };
  }
};
</script>
