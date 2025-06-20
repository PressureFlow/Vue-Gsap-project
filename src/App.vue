<script setup>
import gsap from 'gsap-trial'
import { ScrollSmoother } from 'gsap-trial/ScrollSmoother'
import ScrollToPlugin from 'gsap-trial/ScrollToPlugin'
import { ScrollTrigger } from 'gsap-trial/ScrollTrigger'
import { onMounted, onUnmounted, watch } from 'vue'
import { RouterLink, RouterView, useRoute } from 'vue-router'

gsap.registerPlugin(ScrollTrigger, ScrollSmoother, ScrollToPlugin)

const route = useRoute()
let ctx, smoother

watch(route, newVal => {
	smoother && smoother.kill()
	smoother = ScrollSmoother.create({
		smooth: 1,
		effects: true,
	})
})

onMounted(() => {
	ctx = gsap.context(() => {
		smoother = ScrollSmoother.create({
			smooth: 1,
			effects: true,
		})
		
	})
})

onUnmounted(() => {
	ctx && ctx.revert()
})
</script>

<template>
	<header class="header">
		<div class="brand">
			<img
				src="https://assets.codepen.io/16327/gsap-logo-light.svg"
				alt=""
				id="brandImg"
			/>
		</div>
		<nav>
			<RouterLink to="/">Home</RouterLink>
			<RouterLink to="/about">About me</RouterLink>
			<RouterLink to="/services">Services</RouterLink>
			<RouterLink to="/contacts">Contacts</RouterLink>
		</nav>
	</header>

	<div id="smooth-wrapper">
		<div id="smooth-content">
			<RouterView />
		</div>
	</div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Titillium+Web:ital,wght@0,200;0,300;0,400;0,600;0,700;0,900;1,200;1,300;1,400;1,600;1,700&display=swap');

* {
	margin: 0;
	padding: 0;
	border: 0;
	box-sizing: border-box;
	font-family: 'Poppins', sans-serif;
}

.header {
	width: 100%;
	height: 80px;
	display: flex;
	padding: 0 20px;
	justify-content: space-between;
	background-color: var(--dark);
	position: fixed;
	top: 0;
	left: 0;
	z-index: 10;
	background-color: rgba(0, 0, 0, 0.5);
	align-items: center;
}

.header .brand {
	height: 100%;
	padding: 10px 0;
}
.header .brand img {
	height: 100%;
}

nav {
	display: flex;
	align-items: end;
	gap: 10px;
}

nav a {
	display: inline-block;
	padding: 0px 25px 1px;
	text-decoration: none;
	color: #eee;
}
nav a:hover {
	color: rgb(232, 162, 31);
}

main {
	width: 100%;
}
</style>
