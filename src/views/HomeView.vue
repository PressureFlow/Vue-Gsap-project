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
		let effectElements = gsap.utils.toArray('[data-speed]')

		effectElements.forEach((el, i) => {
			let speed = parseFloat(el.getAttribute('data-speed'))
			gsap.fromTo(
				el,
				{ y: 0 },
				{
					y: 0,
					ease: 'none',
					scrollTrigger: {
						trigger: el,
						start: 'top bottom',
						end: 'bottom top',
						scrub: true,
						onRefresh: self => {
							let start = Math.max(0, self.start),
								// убедитесь, что нет отрицательных начальных значений (элементов, которые изначально находятся в области просмотра)
								distance = self.end - start,
								end = start + distance / speed
							self.setPositions(start, end)
							self.animation.vars.y = (end - start) * (1 - speed) // обновить значение y на анимации
							self.animation.invalidate().progress(1).progress(self.progress) // принудительно сделать твин недействительным, чтобы принять новое значение
						},
					},
				}
			)
		})
	})
})

onUnmounted(() => {
	ctx && ctx.revert()
})
</script>

<template>
	<main>
		<section class="about-section fader" data-speed=".9" id="about">
			<div class="about-container">
				<div class="fader about-info" data-speed="1.1">
					<h1 class="main-title fader">Predator</h1>
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
			<div class="home-deck-cards" id="deck-cards">
				<div class="fader card">
					<div class="card-image">
						<img src="../../public/1.png" alt="" />
					</div>
					<div class="card-content">
						<div class="card-info">
							<h2 class="">Название:</h2>
							<p>Кол-во товара</p>
						</div>
					</div>
					<div class="card-price">
						<h2>49$</h2>
						<div class="card-icon">
							<svg height="16" width="16" viewBox="0 0 24 24">
								<path
									stroke-width="2"
									stroke="currentColor"
									d="M4 12H20M12 4V20"
									fill="currentColor"
								></path>
							</svg>
						</div>
					</div>
				</div>

				<div class="fader card">
					<div class="card-image">
						<img src="../../public/2.png" alt="" />
					</div>
					<div class="card-content">
						<div class="card-info">
							<h2 class="">Название:</h2>
							<p>Кол-во товара</p>
						</div>
					</div>
					<div class="card-price">
						<h2>49$</h2>
						<div class="card-icon">+</div>
					</div>
				</div>

				<div class="fader card">
					<div class="card-image">
						<img src="../../public/3.png" alt="" />
					</div>
					<div class="card-content">
						<div class="card-info">
							<h2 class="">Название:</h2>
							<p>Кол-во товара</p>
						</div>
					</div>
					<div class="card-price">
						<h2>49$</h2>
						<div class="card-icon">+</div>
					</div>
				</div>

				<div class="fader card">
					<div class="card-image">
						<img src="../../public/4.png" alt="" />
					</div>
					<div class="card-content">
						<div class="card-info">
							<h2 class="">Название:</h2>
							<p>Кол-во товара</p>
						</div>
					</div>
					<div class="card-price">
						<h2>49$</h2>
						<div class="card-icon">+</div>
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
	z-index: 1;
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
	transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}

.products-section {
	height: 100vh;
	background-color: #e8e8e8;
	padding: 30px;
}
.home-deck-cards {
	display: flex;
	justify-content: space-around;
	gap: 1em;
}
.card {
	--card-bg: #ffffff;
	--card-accent: #7c3aed;
	--card-text: #1e293b;
	--card-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.05);

	background: var(--card-bg);
	border-radius: 20px;
	box-shadow: var(--card-shadow);
	border: 1px solid rgba(255, 255, 255, 0.2);
	padding: 20px;
	opacity: 0;
	width: 22%;
	transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
	z-index: 11;
}

.card-price {
	position: relative;
	margin-top: 20px;
}
.card-price h2 {
	font-size: 1.5em;
	font-weight: 500;
}
.card:hover .card-price h2,
.card:hover .card-info h2 {
	color: var(--color-amber-500);
	transition: 0.3s ease;
}
.card:hover .card-info p {
	color: var(--color-gray-950);
	transition: 0.3s ease;
}
.card-icon {
	position: absolute;
	width: 50px;
	height: 50px;
	background-color: var(--color-orange-400);
	border-radius: 50%;
	right: 0;
	bottom: 0;
	color: #eee;
	display: flex;
	align-items: center;
	justify-content: center;
	font-size: larger;
	transform: scale(0.9);
	transition: all 0.3s ease;
}
.card:hover .card-icon svg {
	animation: pulse 1.5s infinite;
}

@keyframes pulse {
	0% {
		transform: scale(1);
	}
	50% {
		transform: scale(1.2);
	}
	100% {
		transform: scale(1);
	}
}

.card-info h2 {
	font-size: 2em;
}
.card-info p {
	font-size: 1em;
	color: var(--color-gray-600);
}
.card:hover {
	transform: translateY(-10px);
	box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1),
		0 10px 10px -5px rgba(0, 0, 0, 0.04);
	border-color: rgba(124, 58, 237, 0.2);
}
.card:hover .card-icon {
	transform: scale(1);
	box-shadow: 0 0 0 4px rgba(124, 58, 237, 0.2);
	cursor: pointer;
}
</style>
