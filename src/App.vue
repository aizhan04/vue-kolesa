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
					<router-view></router-view>
				</div>
			</div>
		</section>
		<Footer></Footer>
		<!-- modal -->

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
import Search from '@/layouts/components/Search.vue';
import User from '@/layouts/components/User.vue';
import Sidebar from '@/layouts/components/Sidebar.vue';
import Footer from '@/layouts/components/Footer.vue';

export default {
	name: 'App',
	components: {
		User,
		Search,
		Sidebar,
		Footer,
	},
	data() {
		return {
			value: '',
		};
	},
	watch: {
		score() {
			this.showCost();
		},
	},
	methods: {
		getImgUrl(item) {
			// eslint-disable-next-line global-require,import/no-dynamic-require,import/extensions
			return require(`./assets/${item}`);
		},
		updateUser(data) {
			this.user = data;
		},
	},
};
</script>

<style lang='scss'>
@import '@/style.css/style.scss';
</style>
