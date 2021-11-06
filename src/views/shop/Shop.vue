<template>
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

		<Modal
			:url="getImgUrl"
			:data="modalData"
			:isOpen="isShowModal"
			@order="setScore"
			@close="closeModal"
		></Modal>
	</div>
</template>

<script>
import HotButtons from './components/HotButtons.vue';
import MyFilter from './components/MyFilter.vue';
import CardItem from './components/CardItem.vue';
import Modal from './components/Modal.vue';

export default {
	name: 'App',
	components: {
		Modal,
		HotButtons,
		MyFilter,
		CardItem,
	},
	data() {
		return {
			isActive: false,
			isShowModal: false,
			activeTabKey: 'all',
			modalData: {},
			tabs: [
				{
					key: 'all',
					name: 'Все товары',
				},
				{
					key: 'clothes',
					name: 'Одежда',
				},
				{
					key: 'accesories',
					name: 'Аксессуары',
				},
			],
		};
	},
	computed: {
		allItems() {
			return [...this.clothes, ...this.accesories].sort(
				(a, b) => Number(b.span) - Number(a.span)
			);
		},
		filterItems() {
			if (this.activeTabKey === 'clothes') {
				return [...this.$store.state.clothes];
			}
			if (this.activeTabKey === 'accesories') {
				return [...this.$store.state.accesories];
			}
			return [
				...this.$store.state.clothes,
				...this.$store.state.accesories,
			].sort((a, b) => Number(b.span) - Number(a.span));
		},
	},
	watch: {
		score() {
			this.showCost();
		},
	},
	mounted() {
		this.fetchClothes();
		this.fetchAcc();
	},
	methods: {
		openCard(data) {
			this.isShowModal = true;
			this.modalData = data;
		},

		closeModal() {
			this.isShowModal = false;
		},
		getImgUrl(item) {
			return require(`@/assets/${item}`);
		},
		handleShowModal(cardItem) {
			this.aciveCardItem = cardItem;
			this.isShowModal = true;
		},
		setSearch(data) {
			this.search = data;
		},
		fetchClothes() {
			this.$store.dispatch('fetchClothesInfo');
		},
		fetchAcc() {
			this.$store.dispatch('fetchAccInfo');
		},
	},
};
</script>
