/* eslint-disable no-mixed-spaces-and-tabs */
<template>
	<div class="main">
		<div class="section_header_wrapper">
			<div class="section_header_wrapper__left">
				<img
					class="section_header_wrapper__main_logo"
					src="@/assets/kolesa_img.svg"
					alt="Logo"
				/>
				<Search
					:modelValue="value"
					@update:modelValue="value = $event"
				></Search>
			</div>
			<User :user="user"></User>
		</div>
		<!-- <div class="section_content_wrapper">
			<div class="sidebar_wrapper">
				<ul>
					<li>
						<a class="sidebar_wrapper__paragraph" href="/">Оргсхема</a>
					</li>
					<li>
						<a class="sidebar_wrapper__paragraph" href="/">Kolesa Team</a>
					</li>
					<li>
						<a class="sidebar_wrapper__paragraph" href="/">Kolesa Shop</a>
					</li>
					<li>
						<a class="sidebar_wrapper__paragraph" href="/">Картина компании</a>
					</li>
					<li>
						<a class="sidebar_wrapper__paragraph" href="/">Новости</a>
					</li>
					<li>
						<a class="sidebar_wrapper__paragraph" href="/">Education</a>
					</li>
					<li>
						<a class="sidebar_wrapper__paragraph" href="/">Guidelines</a>
					</li>
					<li>
						<a class="sidebar_wrapper__paragraph" href="/">Библиотека</a>
					</li>
					<li>
						<a class="sidebar_wrapper__paragraph" href="/">FAQ</a>
					</li>
				</ul>
			</div>
			<div class="main_content">
				<div>
					<img
						class="main_content__banner"
						src="@/assets/banner.jpg"
						alt="sale"
					/>
					<div class="main_content__hot_btn">
						<button class="main_content__plus color1">
							<img src="@/assets/plus.svg" alt="plus" />
							<span class="main_content__text">Получить баллы</span>
						</button>
						<button class="main_content__question color2">
							<img src="@/assets/question.svg" alt="question" />
							<span class="main_content__text">Как получить баллы</span>
						</button>
						<button class="main_content__gift color3">
							<img src="@/assets/podarok.svg" alt="gift" />
							<span class="main_content__text">Подарить баллы</span>
						</button>
					</div>
				</div>
				<div class="color">
					<div class="color__item">
						<input id="blue" type="radio" name="name" />
						<label class="js-color" data-id="allGoods" for="blue"
							>Все товары</label
						>
					</div>
					<div class="color__item">
						<input id="beige" type="radio" name="name" />
						<label class="js-color" data-id="clothes" id="color-2" for="beige"
							>Одежда</label
						>
					</div>
					<div class="color__item">
						<input id="grey" type="radio" name="name" />
						<label
							class="js-color"
							data-id="accessories"
							id="color-3"
							for="grey"
							>Аксессуары</label
						>
					</div>
				</div>
				<div class="main-сatalog catalog">
					<div v-for="item in 3" :key="item" class="catalog__item">
						<div class="catalog__image">
							<img
								src="@/assets/futbolka.jpg"
								alt="Shirt"
								width="330"
								height="330"
							/>
							<span class="catalog__badge">new</span>
						</div>
						<div class="catalog__description">
							<div class="catalog__price">220 баллов</div>
							<h3 class="catalog__title">Футболка "Эволюционируй или cдохни</h3>
							<p class="catalog__size">Размеры S/M/L</p>
							<button
								@click="openModal()"
								class="button catalog__button catalog__button_blue"
							>
								Заказать
							</button>
						</div>
					</div>
				</div>
			</div>
		</div> -->
		<section class="main">
			<div class="container">
				<div class="main__wrapper">
					<Sidebar></Sidebar>
					<div class="main__shop">
						<div class="banner">
							<img
								class="banner__img"
								src="@/assets/banner.jpg"
								alt="Алтернативный текст"
							/>
						</div>
						<HotButtons></HotButtons>
						<!-- <MyFilter v-model="activeTabKey" :tabs="tabs"></MyFilter> -->
						<div class="main__goods main__goods--active">
							<CardItem
								v-for="good in filterItems"
								:data="openCard"
								:good="good"
								:url="getImgUrl"
								:key="good.id"
								:dataCard="modalData"
								@get="openCard"
								@show="handleShowModal"
							>
							</CardItem>
						</div>
						<div class="main__clothes d-none"></div>
						<div class="main__acc d-none"></div>
					</div>
				</div>
			</div>
		</section>
		<Footer></Footer>
		<!-- modal -->
		<Modal
			:url="getImgUrl"
			:data="modalData"
			:isOpen="isShowModal"
			@order="setScore"
			@close="closeModal"
		></Modal>
		<!-- Modal 2 -->
		<div class="overlay__thanks">
			<div class="thanks">
				<h3 class="thanks__title">Заказ успешно оформлен!</h3>
				<p class="thanks__descr">
					Для получения заказа подойди в HR отдел к Дяде Рику
				</p>
				<button class="button__thanks">Круто, вернуться в Kolesa Shop</button>
			</div>
		</div>
	</div>
</template>
<script>
import axios from '@/axios';

import Modal from '@/components/Modal.vue';
import Search from '@/components/Search.vue';
import User from '@/components/User.vue';
import HotButtons from '@/components/HotButtons.vue';
import Sidebar from '@/components/Sidebar.vue';
import Footer from '@/components/Footer.vue';
// import MyFilter from '@/components/MyFilter.vue';
import CardItem from '@/components/CardItem.vue';

export default {
	data: () => ({
		isShowModal: false,
		modalData: {},
		value:
			'',
		user: {},
		// eslint-disable-next-line no-dupe-keys
		modalData: {},
		activeTabKey:
			'all',
	}),
	name:
		'App',
	components: {
		Modal,
		Search,
		User,
		HotButtons,
		Sidebar,
		Footer,
		// MyFilter,
		CardItem,
	},
	tabs: [
		{
			key:
				'all',
			name:
				'Все товары',
		},
		{
			key:
				'clothes',
			name:
				'Одежда',
		},
		{
			key:
				'accesories',
			name:
				'Аксессуары',
		},
	],
	computed: {
		allItems() {
			return [
				...this
					.clothes,
				...this
					.accesories,
			].sort(
				(
					a,
					b,
				) => Number(
					b.span,
				)
					- Number(
						a.span,
					),
			);
		},
		filterItems() {
			if (
				this
					.activeTabKey
				=== 'clothes'
			) {
				return [
					...this
						.clothes,
				];
			}
			if (
				this
					.activeTabKey
				=== 'accesories'
			) {
				return [
					...this
						.accesories,
				];
			}
			return [
				...this
					.clothes,
				...this
					.accesories,
			].sort(
				(
					a,
					b,
				) => Number(
					b.span,
				)
					- Number(
						a.span,
					),
			);
		},
	},
	watch: {
		score() {
			this.showCost();
		},
	},
	mounted() {
		axios.get(
			'templates/-_RLsEGjof6i/data',
		).then(
			(
				response,
			) => {
				this.clothes =					response.data;
				console.log(
					'clothes',
					this
						.clothes,
				);
			},
		);
		axios.get(
			'templates/q3OPxRyEcPvP/data',
		).then(
			(
				response,
			) => {
				this.accesories =					response.data;
				console.log(
					'acc',
					this
						.accesories,
				);
			},
		);
		axios.get(
			'templates/7ZW3y5GAuIge/data',
		).then(
			(
				response,
			) => {
				this.user =					response.data;
				console.log(
					'user',
					this
						.user,
				);
			},
		);
	},
	methods: {
		openCard(
			data,
		) {
			this.openModal();
			this.modalData = data;
		},
		openModal() {
			this.isShowModal = true;
		},
		closeModal() {
			this.isShowModal = false;
		},
		getImgUrl(
			item,
		) {
			// eslint-disable-next-line global-require,import/no-dynamic-require,import/extensions
			return require(`./assets/${item}`);
		},
		myFilter(
			tab,
		) {
			this.activeTabKey =				tab.key;
		},
		handleChange(
			tab,
		) {
			this.activeTabKey =				tab.key;
		},
		handleShowModal(
			cardItem,
		) {
			this.aciveCardItem = cardItem;
			this.isShowModal = true;
		},
		setScore(
			price,
		) {
			this.closeModal();
			if (
				this
					.user
					.score
				< price
			) {
				// eslint-disable-next-line no-alert
				alert(
					'денег нет, иди работай',
				);
			} else {
				this.user.score -= price;
				console.log(
					price,
				);
			}
		},
		setSearch(
			data,
		) {
			this.search = data;
		},
		showCost() {
			// eslint-disable-next-line no-alert
			alert(
				this
					.score,
			);
		},
	},
};
</script>

<style lang='scss'>
@import '@/style.css/style.scss';

// #app {
// 	font-family: Avenir, Helvetica, Arial, sans-serif;
// 	-webkit-font-smoothing: antialiased;
// 	-moz-osx-font-smoothing: grayscale;
// 	text-align: center;
// 	color: #2c3e50;
// 	margin-top: 60px;
// }
</style>
