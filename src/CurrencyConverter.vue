<template>
	<div id="currency-converter-app">
		<input type="text" maxlength="9" v-model="valueToConvert" @input="checkInput" />
		<select id="currency-from">
			<option v-for="c in currencies" :key="c.code" :value="c.code">{{ c.name }} {{ c.symbol }}</option>
		</select>

		<br/><br/>

		<input type="text" v-model="resultValue" readonly />
		<select id="currency-to">
			<option v-for="c in currencies" :key="c.code" :value="c.code">{{ c.name }} {{ c.symbol }}</option>
		</select>
	</div>
</template>

<script>
export default {
	data() {
		return {
			valueToConvert: 0,
			resultValue: 0,
			currencies: [
				{ name: 'Euro', code: 'eur', symbol: '€' },
				{ name: 'US Dollar', code: 'usd', symbol: '$' },
				{ name: 'Yen', code: 'jpy', symbol: '¥' }
			].sort(this.compare),
		}
	},
	methods: {
		compare(a, b) {
			if (a.code < b.code) return -1;
			if (a.code > b.code) return 1;
			return 0;
		},
		checkInput() {
			this.resultValue = this.valueToConvert;
		},
	}
}
</script>

<style scoped>

</style>