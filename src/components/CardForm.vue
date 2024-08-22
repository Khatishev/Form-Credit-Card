<template>
    <div class="container">
        <form @submit.prevent="submitForm">
            <label for="number">Card Number</label>
            <input class="data-entry" type="text" id="number" v-model="cardDetails.number" required maxlength="19" @input="formatNumber">
            <label for="holderName">Card Holder</label>
            <input class="data-entry" type="text" id="holderName" v-model="cardDetails.holderName" @input="toUpperCase" required>
            <div class="fields-container">
                <div class="field">
                    <label for="expirationMonth">Expiration Month</label>
                    <select class="data-selection" id="expirationMonth" v-model="cardDetails.expirationMonth" required>
                        <option value="">Month</option>
                        <option v-for="month in 12" :key="month" :value="month">{{ formatMonth(month) }}</option>
                    </select>
                </div>
                <div class="field">
                    <label for="expirationYear">Expiration Year</label>
                    <select class="data-selection" id="expirationYear" v-model="cardDetails.expirationYear" required>
                        <option value="">Year</option>
                        <option v-for="year in generateYears()" :key="year" :value="year">{{ year }}</option>
                    </select>
                </div>
                <div class="field">
                    <label for="cvv">CVV</label>
                    <input class="data-selection" type="text" id="cvv" v-model="cardDetails.cvv" maxlength="3" @input="formatCVV" required @focus="flipCard" @blur="flipCard">
                </div>
            </div>
            <button type="submit">Submit</button>
        </form>
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
        formatNumber() {
            this.cardDetails.number = this.cardDetails.number.replace(/[^0-9]/g, '').replace(/(\d{4})(?=\d)/g, '$1 ');
        },
        toUpperCase() {
            this.cardDetails.holderName = this.cardDetails.holderName.toUpperCase();
            if (!/^[A-Z\s]+$/.test(this.cardDetails.holderName)) {
                this.cardDetails.holderName = '';
            }
        },
        formatMonth(month) {
            return month ? (month < 10 ? `0${month}` : `${month}`) : '';
        },
        generateYears() {
            const currentYear = new Date().getFullYear();
            const years = [];
            for (let i = 0; i < 10; i++) {
                years.push(currentYear + i);
            }
            return years;
        },
        flipCard() {
            this.cardDetails.isFlipped = !this.cardDetails.isFlipped;
        },
        formatCVV() {
            this.cardDetails.cvv = this.cardDetails.cvv.replace(/[^0-9]/g, '');
        },
        submitForm() {
            this.$emit('submit');
        }
    }
}
</script>