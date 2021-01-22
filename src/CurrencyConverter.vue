<template>
	<div id="currency-converter-app">
		<input type="text" maxlength="9" v-model="valueToConvert" @input="checkInput" />
		<select id="currency-from">
			<option v-for="c in currencies" :key="c.code" :value="c.code">{{ c.name }}</option>
		</select>

		<br/><br/>

		<input type="text" v-model="resultValue" />
		<select id="currency-to">
			<option v-for="c in currencies" :key="c.code" :value="c.code">{{ c.name }}</option>
		</select>
	</div>
</template>

<script>
export default {
	data() {
		return {
			valueToConvert: 0,
			currencies: [
				{ name: 'Euro', code: 'eur' },
				{ name: 'US Dollar', code: 'usd' },
				{ name: 'Yen', code: 'jpy' }
			].sort(this.compare)
		}
	},
	methods: {
		compare(a, b) {
			if (a.code < b.code) return -1;
			if (a.code > b.code) return 1;
			return 0;
		},
		checkInput() {
			console.log(this.valueToConvert);
		},
	}
}
</script>

<style scoped>

</style>