<script setup>
import { ref, computed } from "vue";

const props = defineProps({
  cartItems: { type: Array, default: () => [] }
});

const isOpen = ref(false);
const showCheckout = ref(false);
const selectedShipping = ref(500);

const formatPrice = (num) => {
  return Number(num).toLocaleString('de-DE', { minimumFractionDigits: 2 });
};

const totalItemsCount = computed(() => {
  return props.cartItems.reduce((sum, item) => sum + item.quantity, 0);
});

const totalPrice = computed(() => {
  const itemsTotal = props.cartItems.reduce((sum, item) => {
      return sum + (item.price) * (item.quantity);
    }, 0);
    return formatPrice(itemsTotal + Number(selectedShipping.value));
});

const removeItem = (index) => {
  const item = props.cartItems[index];

  if (item.quantity > 1) {
    item.quantity--;
  } else {
    props.cartItems.splice(index, 1);
  }
};
</script>

<template>
  <div class="cart-wrapper">
    <div v-if="!isOpen" class="cart-trigger" @click="isOpen = true">
      <div class="cart-chip">
        <img src="/pics/chip.svg" alt="Chip" />
        <span class="cart-sidebar__cart-count">
          [{{ totalItemsCount}}]</span>
      </div>
    </div>

    <div class="cart-sidebar" :class="{ open: isOpen }">
      <button class="cart-sidebar__close-btn" @click="isOpen = false">X</button>

      <div v-if="!showCheckout" class="cart-sidebar__order-block">
        <div class="cart-sidebar__header">
          <h2>[ CURRENT_LOAD ]</h2>
        </div>

        <div class="cart-sidebar__user">
          <p>> USER: CYBER_GHOST_2077</p>
        </div>

        <div class="cart-sidebar__table-header">
          <span class="header-name">ITEM</span>
          <span class="cart-qty">QTY</span>
          <span class="cart-price">PRICE</span>
        </div>

        <span v-if="props.cartItems.length === 0" class="blink">[ ACCESSING_ENCRYPTED_DATA... ]</span>

        <div v-else class="cart-sidebar__cart-items-list">
          <div v-for="(item, index) in props.cartItems" :key="index" class="cart-item">
            <div class="item-details">
              <span class="item-name">{{ item.name }}</span>
              <span class="item-qty">{{ item.quantity }}</span>
              <span class="item-price">{{ formatPrice(item.price * item.quantity)}} CR</span>
              <button class="remove-item-btn" @click="removeItem(index)"> - </button>
            </div>
          </div>
        </div>

        <div class="cart-sidebar__footer">
          <p>
            CURRENT_DAMAGE:
            <span class="cart-sidebar__total-price">{{ totalPrice }}</span>
            CREDITS
          </p>
          <button
            class="cart-sidebar__checkout-btn"
            :disabled="totalItemsCount === 0"
            @click="showCheckout = true">
            EXECUTE_TRANSACTION
          </button>
        </div>
      </div>
      <div v-else class="cart-sidebar__checkout-form-block">
        <div
          class="cart-sidebar__back-to-cart-btn"
          @click="showCheckout = false">
          <span class="arrow"> <<< </span>
        </div>

        <div class="cart-sidebar__contact-form">
          <p>AUTHENTICATE_USER_FOR_DELIVERY</p>
          <input
            type="text"
            class="cart-sidebar__input"
            placeholder="FIRST_NAME"/>
          <input
            type="text"
            class="cart-sidebar__input"
            placeholder="SECOND_NAME"
          />
          <input
            type="email"
            class="cart-sidebar__input"
            placeholder="NEURAL_MAIL"
          />
          <input
            type="text"
            class="cart-sidebar__input"
            placeholder="ZONE_ADDRESS"
          />
        </div>

        <div class="shipping-section">
          <p>SELECT_LOGISTIC_METHOD:</p>
          <div class="shipping-options">
            <label class="ship-option">
              <input type="radio" name="shipping" v-model="selectedShipping" value="500" />
              <div class="option-content">
                <span class="delivery-method-name"
                  >ORBITAL_LAUNCH [Heavy Rocket] +500 CR</span>
                <br />
                <small class="method-description"
                  >Arrival in 3 seconds. May incinerate your front porch and the
                  neighbor's cat</small>
              </div>
            </label>
          </div>
          <label class="ship-option">
            <input type="radio" name="shipping" v-model="selectedShipping" value="250" />
            <div class="option-content">
              <span class="delivery-method-name"
                >STAR_WAVE_ROUTING [Quantum Drift]
                <span class="option-price">+250 CR</span></span>
              <br />
              <small class="method-description"
                >Package exists in a state of superposition. You'll receive it
                yesterday and tomorrow simultaneously.</small>
            </div>
          </label>

          <label class="ship-option">
            <input type="radio" name="shipping" v-model="selectedShipping" value="0" />
            <div class="option-content">
              <span class="delivery-method-name"
                >CITADEL_DRONE [Local Selector Only]
                <span class="option-price">FREE</span></span>
              <br />
              <small class="method-description"
                >Only flies in clear weather, zero wind, and if the pilot isn't
                playing video games.</small>
            </div>
          </label>

          <div class="checkout-footer">
            <div class="final-checkout-price">
              TOTAL_DAMAGE: {{ totalPrice }} CREDITS
            </div>
            <button class="confirm-order-btn">CONFIRM_ORDER</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.cart-chip {
  position: fixed;
  right: 40px;
  margin-left: auto;
  display: flex;
  align-items: center;
  gap: 2px;
  z-index: 20;
  cursor: crosshair;
}

.cart-chip img {
  width: 40px;
  height: auto;
  filter: brightness(0) saturate(100%) invert(70%) sepia(12%) saturate(2500%)
    hue-rotate(40deg);
  transition:
    filter 0s ease,
    transform 0s ease;
}

.cart-chip img:hover {
  transform: scale(1.1);
  filter: brightness(0) saturate(100%) invert(30%) sepia(80%) saturate(5000%)
    hue-rotate(280deg);
  cursor: pointer;
  transition:
    filter 0s,
    transform 0s;
}

.cart-sidebar__cart-count {
  color: rgb(155, 254, 7);
}

.cart-sidebar__cart-count:hover {
  color: #ff5aff;
  cursor: pointer;
}

.cart-sidebar {
  position: fixed;
  display: flex;
  flex-direction: column;
  top: 0;
  right: -100%;
  height: 100vh;
  background: rgba(0, 0, 0, 0.95);
  border-left: 2px solid rgb(155, 254, 7);
  padding: 16px;
  transition: right 0.4s cubic-bezier(0.77, 0, 0.175, 1);
}

.cart-sidebar.open {
  right: 0;
  width: 560px;
}

.cart-sidebar__close-btn {
  background: transparent;
  position: absolute;
  color: black;
  top: 14px;
  right: 14px;
  background-color: white;
  transition: all 0.3s ease;
  cursor: pointer;
  z-index: 1001;
}

.cart-sidebar__close-btn:hover {
  background: #ff5aff;
  color: white;
}

.cart-sidebar__header {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: crosshair;
  margin-bottom: 20px;
  padding-bottom: 20px;
  margin-top: 30px;
}

.cart-sidebar__header h2 {
  margin: 0;
  padding: 0;
  left: 0;
  top: 0;
  position: relative;
  font-size: 1.1rem;
  color: rgb(155, 254, 7);
  letter-spacing: 4px;
  font-weight: lighter;
}

.cart-sidebar__table-header {
  display: flex;
  justify-content: space-between;
  border-bottom: 2px solid #ff00ff;
  padding: 10px 0;
  padding-left: 10px;
}

.cart-sidebar__user {
  display: flex;
  flex-direction: column;
  color: #00ff41;
  font-size: 0.9rem;
  padding-bottom: 10px;
}

.item-details {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
  flex-grow: 1;
  font-size: 0.9rem;
  padding-left: 10px;
  padding-bottom: 10px;
}

.header-name, .item-name {
  flex: 4;
  text-align: left;
}

.cart-qty, .item-qty {
  flex: 1;
  text-align: center;
}

.cart-price, .item-price {
  flex: 2;
  text-align: right;
  padding-right: 14px;
}

.cart-price {
  padding-right: 40px;
}

.remove-item-btn {
  background: none;
  border: 1px solid #ff00ff;
  color: #ff00ff;
  cursor: pointer;
  padding: 2px 6px;
  flex-shrink: 0;
}

.blink {
  animation: blinker 1.5s linear infinite;
  display: flex;
  justify-content: center;
  padding-top: 40px;
  font-size: 0.9rem;
}

@keyframes blinker {
  50% {
    opacity: 0;
  }
}

.cart-sidebar__back-to-cart-btn {
  display: flex;
  color: rgb(155, 254, 7);
  cursor: pointer;
  position: absolute;
  margin: 14px;
  left: 14px;
  top: 0;
}

.cart-sidebar__back-to-cart-btn .arrow {
  font-size: 1.4rem;
}

.arrow:hover {
  color: #ff00ff;
  transform: translateX(-5px);
}

.cart-sidebar__footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  bottom: 50px;
  position: absolute;
  left: 0;
  right: 0;
  margin: 0 auto;
}

.cart-sidebar__checkout-btn {
  color: white;
  border: none;
  padding: 10px;
  margin-top: 10px;
  background: #ff00ff;
  border-radius: 10px;
  cursor: pointer;
  font-family: "Orbitron", monospace;
  font-size: 0.9rem;
}

.cart-sidebar__checkout-btn:hover {
  background: rgb(155, 254, 7);
  color: black;
}

.cart-sidebar__checkout-btn:disabled {
  opacity: 0.3;
  filter: grayscale(1);
  cursor: not-allowed;
}

.cart-sidebar .cart-sidebar__checkout-form-block input,
.cart-sidebar .cart-sidebar__checkout-form-block button,
.cart-sidebar .cart-sidebar__checkout-form-block label {
  font-family: "Share Tech Mono", monospace;
  letter-spacing: 1px;
  font-size: 1rem;
}

.cart-sidebar__checkout-form-block {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  align-items: center;
  justify-content: center;
  width: 100%;
  padding-top: 20px;
  padding-left: 20px;
}

.cart-sidebar__contact-form {
  display: flex;
  flex-direction: column;
  width: 300px;
  gap: 10px;
  align-items: center;
  margin: 0 auto;
}

.cart-sidebar__contact-form p {
  font-size: 1rem;
}

.cart-sidebar__contact-form input {
  background-color: #061f02;
  color: white;
  width: 100%;
  padding: 8px;
  border: 1px solid #00ff41;
  caret-color: #ff00ff;
}

.shipping-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 60px;
}

.shipping-section p {
  font-size: 1rem;
}

.ship-option input[type="radio"] {
  appearance: none;
  -webkit-appearance: none;
  margin: 0;
  width: 20px;
  height: 20px;
  border: 2px solid #ff00ff;
  background: #061f02;
  cursor: pointer;
  position: relative;
  flex-shrink: 0;
  margin-top: 5px;
}

.ship-option input[type="radio"]:checked {
  background-color: rgb(155, 254, 7);
  border-color: rgb(155, 254, 7);
  box-shadow: 0 0 10px rgb(155, 254, 7);
}

.ship-option input[type="radio"]:checked::after {
  content: "X";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: black;
  font-size: 14px;
  font-weight: bold;
}

.method-description {
  font-style: italic;
  color: #888;
  text-align: center;
  font-size: 0.7rem;
}

.ship-option {
  display: flex;
  padding: 14px;
  cursor: pointer;
}

.delivery-method-name {
  color: #ff00ff;
  font-family: "", monospace;
  font-size: 0.95rem;
}

.option-content {
  padding: 5px;
}

.option-price {
  color: #ff00ff;
  margin-left: 5px;
}

.final-checkout-price {
  width: auto;
  display: flex;
  justify-content: center;
  text-align: center;
  white-space: nowrap;
}

.checkout-footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  margin: 120px;
}

.confirm-order-btn {
  display: block;
  margin: 0 auto;
  background-color: #ff00ff;
  color: white;
  border-radius: 10px;
  padding: 10px;
  border: none;
  cursor: pointer;
}

.confirm-order-btn:hover {
  background-color: rgb(155, 254, 7);
  color: black;
}
</style>
