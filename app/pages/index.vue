<script setup>
import { ref } from "vue";
import ProductCard from "~/components/ProductCard.vue";
import TheNavBar from "~/components/TheNavBar.vue";
import TheShoppingCart from "~/components/TheShoppingCart.vue";

const products = [
  {
    id: 1,
    name: "UNIVERSAL REBOOT",
    img: "/pics/neon-button.jpg",
    description: `Did you ruin your life? Did you say something awkward 5 years ago? Buy this. It won't fix your past, but it will make the screen go black for a few seconds, which is basically the same thing.`,
    price: 1200,
    displayPrice: "1.200.00 CREDITS",
  },
  {
    id: 2,
    name: "MEETING-FREE ZONE",
    img: "/pics/neon-calendar.jpg",
    description: `Mondays are canceled forever. This calendar automatically deletes all 'quick syncs' and 'sync-ups'.`,
    price: 1007,
    displayPrice: "1.007.00 CREDITS",
  },
  {
    id: 3,
    name: "ETERNITY TIME",
    img: "/pics/neon-clock.jpg",
    description: `Five minutes in reality, five centuries in your dreams. Warning: Side effects include waking up in 2077.`,
    price: 5000.99,
    displayPrice: "5.000.99 CREDITS",
  },
  {
    id: 4,
    name: "REMOTE FOR REMOTE",
    img: "/pics/neon-controller.jpg",
    description: `For those who are so lazy, need a controller to find their controller. Peak human evolution.`,
    price: 422.04,
    displayPrice: "422.04.00 CREDITS",
  },
  {
    id: 5,
    name: "REMOTE PUNCH",
    img: "/pics/neon-fist.jpg",
    description: ` Annoyed by someone? Purchase now and a high-speed drone will deliver a physical 'dislike' directly to their face.`,
    price: 699.99,
    displayPrice: "699.99.00 CREDITS",
  },
  {
    id: 6,
    name: "THE VOID V.1.0",
    img: "/pics/neon-frame.jpg",
    description: `Don't want to buy anything? Fine. Buy NOTHING for only 99.99 Credits! It’s limited edition nothing, though.`,
    price: 9999.99,
    displayPrice: "99.99.99 CREDITS",
  },
  {
    id: 7,
    name: "RENT A MATE",
    img: "/pics/neon-friend.jpg",
    description: `A 100% loyal companion who won't ghost you. Mainly because it's physically impossible for them to leave the box.`,
    price: 1900.0,
    displayPrice: "19.00.00 CREDITS",
  },
  {
    id: 8,
    name: "THE ALARM SILENCER",
    img: "/pics/neon-hammer.jpg",
    description: `The most effective 'Snooze' button on the market. Guarantees your alarm clock will never disturb you again. Ever.`,
    price: 249.9999,
    displayPrice: "249.99.99 CREDITS",
  },
  {
    id: 9,
    name: "PLACEBO MAX+",
    img: "/pics/neon-pills.jpg",
    description: ` Guaranteed to increase your productivity by 0%. But hey, look at how cool and green they glow!`,
    price: 1001.99,
    displayPrice: "1.001.99 CREDITS",
  },
  {
    id: 10,
    name: "BOX OF REGRETS",
    img: "/pics/neon-gift.jpg",
    description: `Could be a new GPU, could be a pile of digital trash. Only one way to find out! (Strictly non-refundable).`,
    price: 10.990,
    displayPrice: "10.99.00 CREDITS",
  },
  {
    id: 11,
    name: "HOLY LUXURY",
    img: "/pics/neon-sock.jpg",
    description: `Pre-damaged for your convenience. The hole is strategically placed for maximum toe-ventilation and 'street cred'.`,
    price: 9999.0,
    displayPrice: "9.999.00 CREDITS",
  },
  {
    id: 12,
    name: "DIHYDROGEN MONOXIDE [PRIME]",
    img: "/pics/neon-water.jpg",
    description: `Premium, organic, artisanal liquid oxygen-hydrogen blend. We took ordinary water and put it in a glowing bottle. Now it’s 500% more expensive and 100% more blue.`,
    price: 445.5099,
    displayPrice: "445.50.99 CREDITS",
  },
];

const titleText = "welcome to our chaotic Pink Market";
const titleLetters = titleText.split("");

const cartItems = ref([]);

function addToCart(product) {
  const existingItem = cartItems.value.find(
    (item) => item.name === product.name,
  );

  if (existingItem) {
    existingItem.quantity++;
  } else {
    cartItems.value.push({ ...product, quantity: 1 });
  }
}
</script>

<template>
  <h3 class="matrix-title">
    <span
      v-for="(letter, index) in titleLetters"
      :key="index"
      class="matrix-letter"
      :style="{ animationDelay: `${index * 0.1}s` }"
    >
      {{ letter === " " ? "\u00A0" : letter }}
    </span>
    <span
      class="matrix-title__block"
      :style="{ animationDelay: `${titleLetters.length * 0.1}s` }"
    ></span>
  </h3>
  <div>
    <TheNavBar :items="navBarItems" />
    <TheShoppingCart :cart-items="cartItems" />

    <section class="market-grid">
      <ProductCard
        v-for="item in products"
        :key="item.id"
        :name="item.name"
        :image="item.img"
        :desc="item.description"
        :price="item.displayPrice"
        :originalPrice="item.price"
        @addToCart="addToCart"
      />
    </section>
  </div>
</template>

<style>
.market-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  border-radius: 10px;
  max-width: 1200px;
  margin: 20px auto;
  gap: 1rem;
  padding-top: 120px;
  padding-bottom: 60px;
  align-items: start;
}

.matrix-title {
  display: flex;
  position: absolute;
  left: 50%;
  margin-top: 10px;
  transform: translateX(-50%);
  justify-content: center;
  font-size: 1rem;
  font-weight: lighter;
  letter-spacing: 1px;
  text-shadow: 0 0 10px rgba(155, 254, 7, 0.849);
}

.matrix-title__block {
  display: inline-block;
  width: 16px;
  background-color: rgba(155, 254, 7, 0.748);
  margin-left: 5px;
  vertical-align: middle;
  opacity: 0;
  animation: blink 1s infinite steps(1);
  box-shadow: 0 0 10px rgba(155, 254, 7, 0.7);
}

.matrix-letter {
  display: inline-block;
  opacity: 0;
  transform: translateX(-20px);
  animation: dropIn 0.01s forwards;
}

@keyframes blink {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0;
  }
}

@keyframes dropIn {
  0% {
    opacity: 0;
    transform: translateX(-20px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
    text-shadow: 0 0 10px rgba(155, 254, 7, 0.849);
  }
}
</style>
