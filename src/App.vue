<template>
  <div id="app">
    <CardDisplay :cardDetails="cardDetails" />
    <CardForm :cardDetails="cardDetails" @submit="submitForm" />
  </div>
</template>

<script>
import CardDisplay from './components/CardDisplay.vue';
import CardForm from './components/CardForm.vue';

export default {
  components: {
    CardDisplay,
    CardForm
  },
  data() {
    return {
      isFlipped: false,
      cardDetails: {
        number: '',
        holderName: '',
        expirationMonth: '',
        expirationYear: '',
        cvv: ''
      }
    }
  },
  methods: {
    submitForm() {
      alert('Data received!');
    }
  }
}
</script>