<template>
	<div class="field">
		<div class="filed__title">
			<slot name="title"></slot>
		</div>
		<div class="field__inp" :class="show ? 'focus' : ''" @click="show = !show">
			<div :class="isEmptyTitle === 'Язык' ? 'field__current' : ''">
				<slot name="current">
					{{ isEmptyTitle }}
				</slot>
			</div>
			<div class="filed__drop">
				<svg
					width="30"
					height="30"
					viewBox="0 0 30 30"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						d="M15 17.5858L21.2929 11.2929C21.6834 10.9024 22.3166 10.9024 22.7071 11.2929C23.0976 11.6834 23.0976 12.3166 22.7071 12.7071L15.7071 19.7071C15.3166 20.0976 14.6834 20.0976 14.2929 19.7071L7.29289 12.7071C6.90237 12.3166 6.90237 11.6834 7.29289 11.2929C7.68342 10.9024 8.31658 10.9024 8.70711 11.2929L15 17.5858Z"
						fill="black"
					/>
					<mask
						id="mask0"
						mask-type="alpha"
						maskUnits="userSpaceOnUse"
						x="7"
						y="11"
						width="16"
						height="9"
					>
						<path
							d="M15 17.5858L21.2929 11.2929C21.6834 10.9024 22.3166 10.9024 22.7071 11.2929C23.0976 11.6834 23.0976 12.3166 22.7071 12.7071L15.7071 19.7071C15.3166 20.0976 14.6834 20.0976 14.2929 19.7071L7.29289 12.7071C6.90237 12.3166 6.90237 11.6834 7.29289 11.2929C7.68342 10.9024 8.31658 10.9024 8.70711 11.2929L15 17.5858Z"
							fill="white"
						/>
					</mask>
					<g mask="url(#mask0)">
						<rect width="30" height="30" fill="#0880AE" />
					</g>
				</svg>
			</div>
		</div>

		<slot name="errors"></slot>

		<div v-if="show" class="field__body">
			<div
				class="field__item"
				v-for="lang in langs"
				:key="lang.value"
				@click="onSelect(lang.title)"
			>
				{{ lang.title }}
			</div>
		</div>
	</div>
</template>

<script>
import { computed, ref } from "vue";
export default {
	props: {
		langs: {
			type: Array,
			default: () => [],
		},
	},

	setup(props, { emit }) {
		const show = ref(false);
		const title = ref("");

		const isEmptyTitle = computed(() => (title.value ? title.value : "Язык"));

		const onSelect = (name = "Язык") => {
			title.value = name;
			emit("selectLang", title.value);
			show.value = false;
		};

		return { show, onSelect, isEmptyTitle, title };
	},
};
</script>

<style scoped>
.field {
	position: relative;
}

.error {
	position: absolute;
	left: 0;

	font-weight: normal;
	font-size: 14px;
	line-height: 18px;
	color: #ff7171;
}

.filed__title {
	display: block;
	margin-bottom: 7px;

	font-weight: 500;
	font-size: 16px;
	line-height: 21px;
	color: #756f86;
}

.field__inp {
	display: flex;
	align-items: center;
	justify-content: space-between;

	width: 100%;
	height: 52px;
	padding: 11px;
	margin-bottom: 4px;

	background: #ffffff;
	border: 1px solid #dbe2ea;
	box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
	border-radius: 6px;
	font-size: 16px;
	line-height: 21px;
	color: #2c2738;
}

.field__inp.focus {
	border: 2px solid #0880ae;
}

.field__inp:active {
	border: 2px solid #0880ae;
}

.filed__drop {
	width: 30px;
	height: 30px;
}

.field__body {
	position: absolute;
	top: 92px;
	left: 0;
	z-index: 100;
}

.field__current {
	color: #7c9cbf;
}

.field__body {
	width: 100%;
	padding: 12px 0;

	background: #ffffff;
	border: 1px solid #dbe2ea;
	box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04),
		0px 20px 20px rgba(44, 39, 56, 0.04);
	border-radius: 6px;
}

.field__item {
	padding: 12px 15px;
	transition: all 0.2s linear;
	cursor: pointer;
}

.field__item:hover {
	background: #ebf4f8;
}
</style>
