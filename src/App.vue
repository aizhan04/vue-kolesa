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
						<MyFilter v-model="activeTabKey" :tabs="tabs"></MyFilter>
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
		<!-- <div class="overlay__thanks">
			<div class="thanks">
				<h3 class="thanks__title">Заказ успешно оформлен!</h3>
				<p class="thanks__descr">
					Для получения заказа подойди в HR отдел к Дяде Рику
				</p>
				<button class="button__thanks">Круто, вернуться в Kolesa Shop</button>
			</div>
		</div> -->
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
import MyFilter from '@/components/MyFilter.vue';
import CardItem from '@/components/CardItem.vue';

export default {
	name:
		'App',
	components: {
		Modal,
		User,
		Search,
		Sidebar,
		HotButtons,
		MyFilter,
		CardItem,
		Footer,
	},
	data() {
		return {
			value:
				'',
			isActive: false,
			isShowModal: false,
			activeTabKey:
				'all',
			modalData: {},
			score: 500,
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
			user: [],
		};
	},
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
				alert(
					'отказано',
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
</style>
