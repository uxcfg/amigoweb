<template>
	<div class="field" :class="$attrs.сclass">
		<label :for="$attrs.id">
			<slot name="label"></slot>
		</label>

		<div class="field__wrap">
			<input
				:id="$attrs.id"
				:type="type"
				:value="modelValue"
				v-bind="$attrs"
				:placeholder="$attrs.placeholder"
				@input="(e) => $emit('update:modelValue', e.target.value)"
			/>
		</div>

		<slot name="errors"></slot>
	</div>
</template>

<script>
export default {
	inheritAttrs: false,
	props: {
		type: {
			type: String,
			default: "text",
		},

		modelValue: {
			type: String,
			default: "",
		},
	},
};
</script>

<style scoped>
.field {
	position: relative;
}

.field__wrap {
	height: 52px;
}

.error {
	position: absolute;
	bottom: -28px;
	left: 0;

	font-weight: normal;
	font-size: 14px;
	line-height: 18px;
	color: #ff7171;
}

.field label {
	display: block;
	margin-bottom: 7px;

	font-weight: 500;
	font-size: 16px;
	line-height: 21px;
	color: #756f86;
}

.field input {
	width: 100%;
	padding: 15px;

	height: 100%;
	max-height: 56px;

	background: #ffffff;
	border: 1px solid #dbe2ea;

	box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
	border-radius: 6px;
}

.field input:focus {
	border: 2px solid #0880ae;
}

.field input:focus .form__wrap {
	background-color: #756f86;
}
.field input::placeholder {
	font-size: 16px;
	line-height: 20.8px;
	color: #7c9cbf;
}
</style>
