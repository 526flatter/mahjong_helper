<template>
	<div>
		
	</div>
</template>

<script>
export default {
	name: 'SelectorWithUnit',
	props: ['unit', 'candidates', 'value'],
	methods: {
		changeValue: function(event) {
			console.log(event)
			this.$emit('input', event.target.value)
		}
	}
}
</script>

<style lang="scss" scoped>
div {
	display: flex;
	justify-content: center;
}
</style>
