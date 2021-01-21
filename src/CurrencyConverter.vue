<template>
	<div id="currency-converter-app">
		<input type="text" maxlength="9" v-model="valueToConvert" @input="checkInput" />
		<input type="button" value="Convert" />
	</div>
</template>

<script>
export default {
	data() {
		return {
			valueToConvert: 0
		}
	},
	methods: {
		checkInput() {
			console.log(this.valueToConvert);
		}
	}
}
</script>

<style scoped>

</style>