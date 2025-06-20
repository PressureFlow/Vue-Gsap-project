<script setup>
import gsap from 'gsap-trial'
import ScrollToPlugin from 'gsap-trial/ScrollToPlugin'
import { ScrollTrigger } from 'gsap-trial/ScrollTrigger'
import { onMounted, onUnmounted } from 'vue'

gsap.registerPlugin(ScrollTrigger, ScrollToPlugin)

let ctx

onMounted(() => {
	ctx = gsap.context(() => {
		const cards = gsap.utils.toArray('.card')
		cards.forEach(card => {
			gsap.to(card, {
				opacity: 1,
				scrollTrigger: {
					trigger: card,
					start: 'top 80%',
					end: 'top 40%',
					scrub: true,
					markers: true,
				},
			})
		})
		const buttons = document.querySelectorAll('.btn')
		buttons.forEach(button => {
			button.addEventListener('click', () => {
				gsap.to(window, {
					duration: 1,
					scrollTo: { y: '#products', offsetY: 50 },
				})
			})
		})
	})
})

onUnmounted(() => {
	ctx && ctx.revert()
})
</script>

<template>
	<main>
		<section class="about-section" data-speed="1" id="about">
			<div class="about-container">
				<div class="about-info">
					<h1 class="main-title">Predator</h1>
					<h2>Predator: Высший уровень рыболовной охоты</h2>
					<p>
						Рыбалка – это больше, чем просто хобби. Это вызов, азарт, и
						стремление к победе. В магазине "Predator" мы понимаем это как никто
						другой. Мы предлагаем снаряжение для настоящих хищников – тех, кто
						не боится преследовать свою добычу и добиваться успеха. У нас вы
						найдете всё необходимое, чтобы выйти за пределы обычного и поймать
						трофей своей мечты. Присоединяйтесь к охоте – выбирайте "Predator"!
					</p>
					<button class="btn">Перейти</button>
				</div>
			</div>
		</section>
		<section class="products-section" id="products">
			<div class="">
				<div class="home-deck-cards delayed" id="deck-cards">
					<div class="fader card">
						<div class="card-image">
							<img src="../../public/1.png" alt="" />
						</div>
						<div class="card-info">
							<h2 class="">Название:</h2>
							<p>Кол-во товара</p>
						</div>
					</div>

					<div class="fader card card2">
						<div class="card-image">
							<img src="../../public/2.png" alt="" />
						</div>
						<div class="card-info">
							<h2 class="">Название:</h2>
							<p>Кол-во товара</p>
						</div>
					</div>

					<div class="fader card">
						<div class="card-image">
							<img src="../../public/3.png" alt="" />
						</div>
						<div class="card-info">
							<h2 class="">Название:</h2>
							<p>Кол-во товара</p>
						</div>
					</div>

					<div class="fader card">
						<div class="card-image">
							<img src="../../public/4.png" alt="" />
						</div>
						<div class="card-info">
							<h2 class="">Название:</h2>
							<p>Кол-во товара</p>
						</div>
					</div>
				</div>
			</div>
		</section>
	</main>
</template>

<style scoped>
.main-title {
	text-transform: uppercase;
	font-size: 6vw;
	font-family: 'Titillium', sans-serif;
	line-height: 12vh;
	color: rgb(211, 137, 0);
	font-weight: bold;
}
.about-container {
	background-image: url(../../public/PersonFisher/2.jpeg);
	background-size: cover;
	height: 90vh;
	display: flex;
	align-items: center;
}

.about-info {
	color: #eee;

	margin-left: 10vw;
	padding: 20px;
	border-radius: 10px;
	width: 35vw;
	min-width: 300px;
	border-radius: 30px;
	background: #1d1d1d;
	gap: 0.5em;
	display: flex;
	flex-direction: column;
	box-shadow: 0px 7px 8px 0px rgba(34, 60, 80, 0.2);
	align-items: center;
}

.about-info h2,
h1 {
	text-align: center;
}
.about-info p {
	font-size: 18px;
	margin: 20px;
	text-align: justify;
}
.btn {
	padding: 15px;
	background-color: #eee;
	color: #1d1d1d;
	width: 50%;
	text-align: center;
	border-radius: 20px;
}
.btn:hover {
	padding: 15px;
	background-color: #ff9100;
	color: #ffffff;
}
.home-deck-cards {
	display: flex;
	justify-content: space-between;
	margin: 20px;
	height: 100vh;
	gap: 1.5em;
}
.card {
	border-radius: 20px;
	box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.5);
	height: 600px;
	padding: 20px;
	display: flex;
	flex-direction: column;
	opacity: 0;
}
</style>
