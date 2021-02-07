<template>
	<div class="contact-form">
		<div class="contact-form__header">
			<h1 class="contact-form__title">Регистрация</h1>
			<p class="contact-form__subtitle">
				Уже есть аккаунт? <a href="#">Войти</a>
			</p>
		</div>

		<form class="form" @submit.prevent="onSubmitForm">
			<AppInput
				v-model.trim="vv.name.$model"
				id="name"
				placeholder="Введите Ваше имя"
				сclass="form__field"
			>
				<template #label>
					Имя
				</template>

				<template #errors>
					<p v-if="vv.name.required.$invalid" class="error">
						Поле обязательное для заполнения
					</p>
					<p v-if="vv.name.nameValid.$invalid" class="error">
						Введено не корректное значение
					</p>
				</template>
			</AppInput>

			<AppInput
				v-model.trim="vv.email.$model"
				id="email"
				placeholder="Введите ваш email"
				сclass="form__field"
			>
				<template #label>
					Еmail
				</template>

				<template #errors>
					<p v-if="vv.email.required.$invalid" class="error">
						Поле обязательное для заполнения
					</p>
					<p v-if="vv.email.email.$invalid" class="error">
						Введено не корректное значение
					</p>
				</template>
			</AppInput>

			<AppInput
				v-model.trim="vv.phone.$model"
				id="phone"
				placeholder="Введите номер телефона"
				сclass="form__field"
			>
				<template #label>
					Номер телефона
				</template>

				<template #errors>
					<p v-if="vv.phone.phoneValid.$invalid" class="error">
						Введено не корректное значение<br />
					</p>
				</template>
			</AppInput>

			<AppSelect class="form__field" :langs="langs" @selectLang="onSelectLang">
				<template #title>Язык</template>
				<template #placeholder>Язык</template>
				<template #errors>
					<p v-if="vv.lang.required.$invalid" class="error">
						Поле обязательное для заполнения
					</p>
				</template>
			</AppSelect>

			<AppRules @checkRules="onCheckRules" class="form__field">
				<template #errors>
					<p v-if="vv.rules.rulesValid.$invalid" class="error">
						Поле обязательное для заполнения
					</p>
				</template>
			</AppRules>
			<AppBtn :disabled="!validForm">
				Зарегистрироваться
			</AppBtn>
		</form>
	</div>
</template>

<script>
import useVuelidate from "@vuelidate/core";
import { required, email, helpers } from "@vuelidate/validators";
import { computed, reactive, ref } from "vue";
import AppInput from "@/components/UI/AppInput.vue";
import AppSelect from "@/components/UI/AppSelect.vue";
import AppRules from "./UI/AppRules.vue";
import AppBtn from "./UI/AppBtn.vue";
export default {
	components: { AppInput, AppSelect, AppRules, AppBtn },

	setup() {
		const user = reactive({
			name: "",
			email: "",
			phone: "",
			lang: "",
			rules: "",
		});
		const name = ref("");

		const validForm = computed(() => {
			return Object.values(user).every((el) => {
				return Boolean(el) == true;
			});
		});

		const langs = ref([
			{ title: "Русский", value: "russian" },
			{ title: "Английский", value: "english" },
			{ title: "Китайский", value: "chinese" },
			{ title: "Испанский", value: "spanish" },
		]);

		const onCheckRules = (bool) => {
			user.rules = bool;
		};

		const onSelectLang = (lang) => {
			user.lang = lang;
		};

		const onSubmitForm = () => {
			vv.value.$touch();

			if (vv.value.$invalid && vv.value.$error) return;

			const clearUser = {
				name: "",
				email: "",
				phone: "",
				lang: "",
				rules: "",
			};

			alert("form submit");
			Object.assign(user, clearUser);
			vv.value.$reset();
		};

		const nameValid = (value) =>
			!helpers.req(value) || /^[a-zа-я\s\-]+$/i.test(value);

		const phoneValid = (value) =>
			/(^\+\d\s?\d{3}\s?\d{3}(\-?\d{2}){2}$|^\+\d\s?\(\d{3}\)\s?\d{3}(\-?\d{2}){2}$)/.test(
				value
			);

		const rulesValid = (value) => value === true;

		const validate = {
			email: { email, required },
			name: {
				required,
				nameValid,
			},
			phone: { phoneValid },
			rules: { rulesValid },
			lang: { required },
		};

		const vv = useVuelidate(validate, user);

		return {
			user,
			langs,
			onCheckRules,
			name,
			onSelectLang,
			onSubmitForm,
			vv,
			validForm,
		};
	},
};
</script>

<style>
.contact-form {
	width: 100%;
	max-width: 400px;
	min-width: 360px;

	padding: 40px 30px;
	border-radius: 24px;
	background-color: #fff;
	box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.02),
		0px 32px 64px rgba(44, 39, 56, 0.04);
}

.contact-form__header {
	margin-bottom: 56px;
}

.contact-form__title {
	font-weight: bold;
	font-size: 34px;
	color: #2c2738;
	line-height: 44px;

	margin-bottom: 8px;
}

.contact-form__subtitle {
	font-weight: normal;
	font-size: 16px;
	line-height: 22px;

	color: #2c2738;
}

.contact-form__subtitle a {
	font-weight: normal;
	font-size: 16px;

	color: #0880ae;
}

.form__field {
	margin-bottom: 34px;
}
</style>
