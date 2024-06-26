<template>
  <div class="card">
    <div v-if="loading" class="loader"></div>
    <img v-else :src="product.image" alt="Product Image" />
    <div class="desc">
      <div>
        <div style="margin-bottom: 10px">
          <div v-if="loading" class="skeleton-title"></div>
          <div v-else class="title" :class="'title-' + productCategory">{{ product.title }}</div>
        </div>
        <div style="display: flex; justify-content: space-between; margin-bottom: 10px">
          <div>
            <div v-if="loading" class="skeleton-category"></div>
            <div v-else class="category">{{ product.category }}</div>
          </div>
          <div class="rating">
            <div>
              <div v-if="loading" class="skeleton-rating"></div>
              <div v-else>{{ product.rating.rate }}/5</div>
            </div>
            <div class="rating">
              <div v-if="loading" class="skeleton-rating"></div>
              <template v-else>
                <div v-for="index in 5" :key="index" class="circle" :class="{ [`actived${productCategory}`]: index <= Math.round(product.rating.rate) }"></div>
              </template>
            </div>
          </div>
        </div>
        <hr />
      </div>

      <div class="description-container">
        <div v-if="loading" class="skeleton-description"><span></span><span></span><span></span><span></span></div>
        <div v-else class="description">{{ product.description }}</div>
      </div>

      <div>
        <hr />
        <div v-if="loading" class="skeleton-price"></div>
        <div v-else class="price" :class="'price-' + productCategory">$ {{ product.price }}</div>
        <div class="button-action">
          <button :class="'buy-now-' + productCategory">Buy now</button>
          <button @click="fetchNextProduct" :class="'next-product-' + productCategory">Next product</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    product: Object,
    loading: Boolean,
    productCategory: String,
  },
  methods: {
    fetchNextProduct() {
      this.$emit("fetchNextProduct");
    },
  },
};
</script>

<style scoped>
.card {
  background-color: var(--color-white);
  font-weight: 500;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.5);
  border-radius: 5px;
  width: 65%;
  height: 75%;
  align-items: center;
  display: grid;
  grid-template-columns: 1fr 2fr;
  padding: 2%;
}

img {
  width: 75%;
  margin: 0 10%;
}

.desc {
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content: space-between;
}

.title {
  font-weight: 600;
  font-size: 25px;
}

.category,
.rating {
  font-weight: 400;
  font-size: 17px;
  color: var(--color-medium-gray);
}

.rating {
  display: flex;
  gap: 5px;
}

.description {
  font-size: 18px;
  font-weight: 400;
  color: var(--color-dark-gray);
}

.description-container {
  min-height: 270px;
}

.price {
  font-size: 28px;
  font-weight: 600;
  margin-top: 5px;
}

.title,
.category,
.rating,
.description,
.price {
  font-family: "Inter";
}
/* end container and card */

/* circle rating */
.circle {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: var(--color-white);
  border: 1px solid gray;
}

.circle.activedwomen-section {
  background-color: var(--color-dark-pink);
}
.circle.activedmen-section {
  background-color: var(--color-dark-blue);
}

/* end circle rating */

/* spin and skeleton loading  */
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.loader {
  border: 16px solid var(--color-light-gray);
  border-top: 16px solid var(--color-dark-blue);
  border-radius: 50%;
  width: 80px;
  height: 80px;
  animation: spin 2s linear infinite;
  margin: auto;
}

.skeleton-title {
  width: 550px;
  height: 19px;
}

.skeleton-category {
  width: 100px;
  height: 20px;
}

.skeleton-rating {
  width: 80px;
  height: 20px;
}

.skeleton-description span:nth-child(1) {
  width: 500px;
  height: 15px;
}
.skeleton-description span:nth-child(2) {
  width: 450;
  height: 15px;
}
.skeleton-description span:nth-child(3) {
  width: 500px;
  height: 15px;
}
.skeleton-description span:nth-child(4) {
  width: 300px;
  height: 15px;
}

.skeleton-price {
  width: 100px;
  height: 30px;
  margin-top: 5px;
}

.skeleton-title,
.skeleton-category,
.skeleton-rating,
.skeleton-description span:nth-child(1),
.skeleton-description span:nth-child(2),
.skeleton-description span:nth-child(3),
.skeleton-description span:nth-child(4),
.skeleton-price {
  animation: pulse 2s infinite ease-in-out;
  display: inline-block;
}

@keyframes pulse {
  0% {
    background-color: #94a3b8;
  }

  50% {
    background-color: #cbd5e1;
  }

  100% {
    background-color: #94a3b8;
  }
}
/* end spin and skeleton loading */

/* button action */
.button-action {
  display: flex;
  justify-content: space-between;
}

button {
  font-family: "Inter";
  border-radius: 3px;
  margin-top: 10px;
  font-size: 20px;
  font-weight: 600;
  width: 48%;
  height: 40px;
  cursor: pointer;
}

.title-men-section,
.circle-men-section,
.price-men-section {
  color: var(--color-dark-blue);
}

.title-women-section,
.circle-women-section,
.price-women-section {
  color: var(--color-dark-pink);
}

.buy-now-men-section {
  border: 3px solid var(--color-dark-blue);
  background-color: var(--color-dark-blue);
  color: var(--color-white);
  transition: 0.1s;
}
.buy-now-women-section {
  border: 3px solid var(--color-dark-pink);
  background-color: var(--color-dark-pink);
  color: var(--color-white);
  transition: 0.1s;
}

.buy-now-men-section:hover,
.buy-now-women-section:hover {
  opacity: 80%;
  font-size: 21px;
  padding-bottom: 5px;
}

.next-product-men-section {
  border: 3px solid var(--color-dark-blue);
  background-color: var(--color-white);
  color: var(--color-dark-blue);
  transition: 0.1s;
}
.next-product-women-section {
  border: 3px solid var(--color-dark-pink);
  background-color: var(--color-white);
  color: var(--color-dark-pink);
  transition: 0.1s;
}

.next-product-men-section:hover,
.next-product-women-section:hover {
  opacity: 80%;
  font-size: 21px;
  padding-bottom: 5px;
}

/* end button action */

@media (max-width: 768px) {
  .card {
    width: 85%;
    grid-template-columns: 1fr;
    padding: 5%;
    min-height: 700px;
    height: auto;
  }

  img {
    width: 70%;
    margin: 20px auto;
  }

  .description-container {
    min-height: auto;
  }

  .desc {
    height: auto;
  }

  .button-action button {
    width: 100%;
    margin-top: 5px;
  }

  .skeleton-title,
  .skeleton-category,
  .skeleton-rating,
  .skeleton-description span:nth-child(1),
  .skeleton-description span:nth-child(2),
  .skeleton-description span:nth-child(3),
  .skeleton-description span:nth-child(4),
  .skeleton-price {
    width: 100px;
    height: 15px;
  }

  .skeleton-price {
    margin-bottom: 20px;
  }
  .price {
    margin-bottom: 20px;
  }
}

@media (max-width: 480px) {
  .card {
    width: 80%;
  }

  .title,
  .category,
  .rating,
  .description,
  .price {
    font-size: smaller;
  }

  .button-action {
    flex-direction: column;
  }

  .button-action button {
    height: 50px;
  }
}
</style>
