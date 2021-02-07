<template>
	<button
		class="btn"
		v-bind="$attrs"
		:class="!$attrs.disabled ? '' : 'disabled'"
	>
		<slot></slot>
	</button>
</template>

<script>
export default {
	inheritAttrs: false,
};
</script>

<style scoped>
.btn {
	width: 100%;
	padding: 18px 10px;

	color: white;
	background: #0880ae;
	box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08),
		0px 4px 8px rgba(44, 39, 56, 0.08);
	border-radius: 6px;
	outline: none;
	border: none;

	transition: box-shadow 0.2s linear;
}

.btn:hover {
	box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.08),
		0px 24px 48px rgba(44, 39, 56, 0.16);
}

.btn:active {
	border: 2px solid rgba(44, 39, 56, 0.86);
}

.disabled {
	background: #dbe2ea;
}
</style>
