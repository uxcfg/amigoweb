<template>
	<div class="container">
		<ContactForm />
	</div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";

export default {
	name: "App",
	components: {
		ContactForm,
	},
};
</script>

<style>
*,
*::before,
*::after {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

:focus,
:active {
	outline: none;
}

ul li,
ol li {
	list-style: none;
}

body {
	font-family: "IBM Plex Sans", sans-serif;
	min-height: 100vh;
	scroll-behavior: smooth;
	line-height: 1;
	color: #2c2738;

	background-color: #e5e5e5;
}

a,
a:visited {
	text-decoration: none;
}

h1,
h2,
h3,
h3,
h5,
h6 {
	font-size: inherit;
	font-weight: 400;
}

img {
	max-width: 100%;
	display: block;
}

input,
button,
textarea,
select {
	font: inherit;
}

button {
	cursor: pointer;
}

.container {
	width: 100%;
	max-width: 1140px;
	min-height: 100vh;
	margin: 0 auto;
	padding: 0 15px;

	display: flex;
	align-items: center;
	justify-content: center;
}
</style>
