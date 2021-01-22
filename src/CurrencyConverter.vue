<template>
	<div id="currency-converter-app">
		<div class="msg" v-if="hasError">{{ this.errorMsg }}</div>

		<input type="text" maxlength="9" v-model="valueToConvert" @input="checkInput" />
		<select v-model="convertFrom" @change="checkInput">
			<option v-for="c in currencies" :key="c.code" :value="c.code">{{ c.name }} {{ c.symbol }}</option>
		</select>

		<br/><br/>

		<input type="text" v-model="resultValue" readonly />
		<select v-model="convertTo" @change="checkInput">
			<option v-for="c in currencies" :key="c.code" :value="c.code">{{ c.name }} {{ c.symbol }}</option>
		</select>
	</div>
</template>

<script>
const ONLY_NUMBERS_REGEX = /^[0-9]+$/;
const ERROR_MSG = 'Invalid input, only numbers are allowed';

export default {
	data() {
		return {
			hasError: false,
			errorMsg: ERROR_MSG,
			valueToConvert: 1,
			resultValue: 0,
			convertFrom: 'eur',
			convertTo: 'usd',
			currencies: [
				{ name: 'Euro', code: 'eur', symbol: '€' },
				{ name: 'US Dollar', code: 'usd', symbol: '$' },
				{ name: 'Yen', code: 'jpy', symbol: '¥' }
			].sort(this.compare),
			conversionRates: {
				eur: { usd: 1.22, jpy: 126.15 },
				usd: { eur: 0.82, jpy: 103.62 },
				jpy: { eur: 0.0079, usd: 0.0097 },
			}
		}
	},
	methods: {
		compare(a, b) {
			if (a.code < b.code) return -1;
			if (a.code > b.code) return 1;
			return 0;
		},
		checkInput() {
			if (!ONLY_NUMBERS_REGEX.test(this.valueToConvert)) {
				this.showErrorMessage();
				return;
			}

			this.convert();
		},
		convert() {
			if (this.convertFrom === this.convertTo) {
				this.resultValue = this.valueToConvert;
				return;
			}

			this.resultValue = this.valueToConvert * this.conversionRates[this.convertFrom][this.convertTo];
		},
		showErrorMessage() {
			this.hasError = true;
		},
	},
	beforeMount() {
		this.checkInput();
	},
}
</script>

<style scoped>

</style>