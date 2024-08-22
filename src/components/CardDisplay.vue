<template>
  <div class="card-container">
    <div class="card" :class="{ flipped: cardDetails.isFlipped }">
      <div class="card-front">
        <div class="card-icons">
          <img class="approximation" src="/src/assets/approximation.png" alt="approximation">
          <img class="chip" src="/src/assets/chip.png" alt="chip">
          <img class="visa" src="/src/assets/visa.png" alt="visa">
        </div>
        <div class="card-number">
          <span class="number">{{ cardDetails.number || 'XXXX XXXX XXXX XXXX' }}</span>
        </div>
        <div class="card-expires">
          <span>EXPIRES</span>
          <div>{{ formatMonth(cardDetails.expirationMonth) || 'MM' }} / {{ cardDetails.expirationYear || 'YY' }}</div>
        </div>
        <div class="card-holder">
          <span class="holder">CARD HOLDER</span>
          <div class="name-holder">{{ cardDetails.holderName || 'FULL NAME' }}</div>
        </div>
      </div>
      <div class="card-back">
        <div class="card-back-content">
          <div class="magnetic-strip"></div>
          <div class="signature-strip">
            <span class="cvv">CVV</span>
            <div class="cvv-box">{{ cardDetails.cvv || 'XXX' }}</div>
          </div>
          <img class="visa-back" src="/src/assets/visa.png" alt="visa">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cardDetails: {
      type: Object,
      required: true
    }
  },
  methods: {
    formatMonth(month) {
      return month ? (month < 10 ? `0${month}` : `${month}`) : '';
    }
  }
}
</script>