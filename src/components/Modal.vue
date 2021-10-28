<template>
	<div class="overlay" :class="{ show: isOpen }" @click="closeModal">
		<div class="modal" @click.stop>
			<div class="modal__left">
				<img class="modal__img" :src="data.mainImage" :alt="data.alt" />
				<div class="modal__thumbnails"></div>
			</div>
			<div class="modal__right">
				<div class="modal__title">{{ data.title }}</div>
				<div class="modal__item-wrapper">
					<div class="modal__item-info">
						<div class="modal__item-price">{{ data.price }} Баллов</div>
						<a href="#" class="main__btn main__btn--yellow" @click="order"
							>Попросить 50 баллов</a
						>
					</div>
					<div class="modal__item-balance">
						<div class="modal__item-supheader">Твой баланс:</div>
						<div class="modal__item-points">50 баллов</div>
					</div>
				</div>
				<form class="modal__form" action="#">
					<div class="colors">
						<h3 class="colors__title">Цвета:</h3>
						<div class="colors__wrapper">
							<input
								class="custom-radio blue visual-hidden"
								type="radio"
								id="blue"
								name="colors"
								checked
							/>
							<label class="label__color" for="blue">Синий</label>
							<input
								class="custom-radio beige visual-hidden"
								type="radio"
								id="beige"
								name="colors"
							/>
							<label class="label__color" for="beige">Бежевый</label>
							<input
								class="custom-radio gray visual-hidden"
								type="radio"
								id="gray"
								name="colors"
							/>
							<label class="label__color" for="grey">Серый</label>
						</div>
					</div>
					<div class="sizes">
						<h3 class="sizes__title">Размер:</h3>
						<div class="sizes__wrapper">
							<input
								class="custom-radio__size visual-hidden"
								type="radio"
								id="small"
								name="sizes"
								checked
							/>
							<label class="label__size" for="small">S</label>
							<input
								class="custom-radio__size visual-hidden"
								type="radio"
								id="medium"
								name="sizes"
							/>
							<label class="label__size" for="medium">M</label>
							<input
								class="custom-radio__size visual-hidden"
								type="radio"
								id="large"
								name="sizes"
							/>
							<label class="label__size" for="large">L</label>
						</div>
					</div>
				</form>
				<div class="details">
					<h3 class="details__title">Детали:</h3>
					<p class="detail__descr">
						{{ data.description }}
					</p>
				</div>
				<div class="question">
					<h3 class="question__title">Как выбрать размер?:</h3>
					<p class="question__txt">Написать дяде Рику для уточнения.</p>
				</div>
			</div>
			<div class="modal__close">
				<img
					class="close__btn"
					src="@/assets/modal_card/close-big.svg"
					alt="close"
					@click="closeModal"
				/>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name:
		'Modal',
	props: {
		isOpen: Boolean,
		data: Object,
		url: Function,
	},
	data() {
		return {
			isShowModal: false,
		};
	},
	methods: {
		closeModal() {
			this.$emit(
				'close',
			);
		},
		order() {
			this.$emit(
				'order',
				this
					.data
					.price,
			);
		},
	},
};
</script>
