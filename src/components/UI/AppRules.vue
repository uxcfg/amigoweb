<template>
	<div class="field">
		<div class="field__checkbox">
			<label
				@click="onRead"
				class="checkbox__field"
				:class="selected ? 'active' : ''"
				for="checkbox"
			>
				<svg
					class="checkbox__field-done"
					:class="selected ? 'active' : ''"
					width="16"
					height="12"
					viewBox="0 0 16 12"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						d="M14.6343 0.634308C14.9467 0.321889 15.4533 0.321889 15.7657 0.634308C16.0781 0.946728 16.0781 1.45326 15.7657 1.76568L6.16567 11.3657C5.85325 11.6781 5.34672 11.6781 5.0343 11.3657L1.0343 7.36568C0.721883 7.05326 0.721883 6.54673 1.0343 6.23431C1.34672 5.92189 1.85325 5.92189 2.16567 6.23431L5.59999 9.66862L14.6343 0.634308Z"
						fill="#0880ae"
					/>
				</svg>
			</label>

			<input class="checkbox__inp" id="checkbox" type="checkbox" />
		</div>

		<div class="field__rules">Принимаю <span>условия</span> использования</div>

		<slot name="errors"></slot>
	</div>
</template>

<script>
import { ref } from "vue";
export default {
	setup(props, { emit }) {
		const selected = ref(false);
		const onRead = () => {
			selected.value = !selected.value;
			emit("checkRules", selected.value);
		};

		return { selected, onRead };
	},
};
</script>

<style scoped>
.field {
	position: relative;
	display: flex;
	align-items: center;
}

.error {
	position: absolute;
	bottom: -20px;
	left: 0;

	font-weight: normal;
	font-size: 14px;
	line-height: 18px;
	color: #ff7171;
}

.checkbox__field {
	display: flex;
	align-items: center;
	justify-content: center;

	width: 28px;
	height: 28px;

	background: #ffffff;
	border: 1px solid #dbe2ea;
	box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
	border-radius: 4px;

	cursor: pointer;
}

.checkbox__field.active {
	border: 2px solid #0880ae;
}

.checkbox__field-done {
	display: none;
}

.checkbox__field-done.active {
	display: flex;
}

.checkbox__inp {
	position: absolute;
	width: 1px;
	height: 1px;
	top: 0;
	right: 0;
	opacity: 0;
}

.field__rules {
	font-weight: 500;
	font-size: 16px;
	line-height: 21px;
	color: #756f86;

	margin-left: 8px;
}

.field__rules span {
	cursor: pointer;
	color: #0880ae;
}
</style>
