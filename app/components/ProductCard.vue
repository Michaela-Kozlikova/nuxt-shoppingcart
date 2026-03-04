<script setup>
import { ref } from "vue";

const props = defineProps({
  name: String,
  image: String,
  desc: String,
  price: String,
  originalPrice: Number,
  active: Boolean,
});

const isActive = ref(false);

const toggleActive = () => { isActive.value = !isActive.value; };

const emit = defineEmits(['addToCart'])

function handleClick(event) {
  event.stopPropagation();

  emit('addToCart', {
    id: props.name,
    name: props.name,
    price: props.originalPrice,
    image: props.image,
    desc: props.desc,
    quantity: 1
  })
};
</script>

<template>
  <div class="product-card" :class="{ active: isActive }" @click="toggleActive">
    <img :src="image" :alt="name" />
    <div class="product-card-description">
      <h3>{{ name }}</h3>
      <p>
        {{ desc }}
        <span class="price">PRICE: {{ price }}</span>
        <button class="buy-button" @click="handleClick">
          [ INJECT-FUNDS ]
        </button>
      </p>
    </div>
  </div>
</template>

<style scoped>
.product-card {
  border-radius: 10px;
  border: 2px solid white;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  width: 100%;
  transition: all 0.3s ease;
}

.product-card:hover {
  cursor: crosshair;
  transform: scale(1.02);
  border-color: rgb(155, 254, 7);
}

.product-card img {
  width: 100%;
  height: 200px;
  display: block;
  object-fit: cover;
}

.product-card-description {
  padding: 14px;
  text-align: center;
}

.product-card-description h3 {
  color: rgb(155, 254, 7);
  margin: 0;
  height: 2rem;
  font-weight: lighter;
  font-size: 1.1rem;
  letter-spacing: 0.02rem;
}

.product-card-description p {
  display: none;
  margin-top: 14px;
  color: white;
  border-top: 1px solid rgb(155, 254, 7);
  padding-top: 10px;
  font-size: 0.9rem;
  line-height: 20px;
}

.product-card.active p {
  display: block;
}

.price {
  display: block;
  margin-top: 20px;
}

.buy-button {
  cursor: pointer;
  margin-top: 10px;
  background-color: rgb(93, 255, 6);
  font-weight: bolder;
}
</style>
