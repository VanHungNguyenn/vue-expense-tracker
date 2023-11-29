<template>
	<h4>Your Balance</h4>
	<h1 class="balance">${{ total }}</h1>
</template>

<script setup>
const props = defineProps({
	total: {
		type: Number,
		required: true,
	},
})
</script>

<style lang="scss" scoped></style>
