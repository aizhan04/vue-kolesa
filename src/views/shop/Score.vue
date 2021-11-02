<template>
	<div class="main__points">
		<div class="breadcrupms">
			<div class="breadcrumps__wrapper">
				<ul class="breadcrumps__list">
					<li class="breadcrumps__list-item">
						<a class="breadcrumps__list-link" href="#" @click="goToShop"
							>Kolesa Shop</a
						>
					</li>
					<li class="breadcrumps__list-item">
						<a class="breadcrumps__list-link" href="#">Как получить баллы</a>
					</li>
				</ul>
			</div>
		</div>
		<div class="main__points-items">
			<h3 class="main__points-title">Как получить баллы</h3>
			<div
				class="main__points-wrapper"
				v-for="(item, idx) in itemList"
				:key="idx"
			>
				<div class="main__points-item">
					<div class="main__points-header">{{ item.title }}</div>
					<div class="main__points-sum">{{ item.balance }}</div>
					<p class="main__points-descr">
						{{ item.descr }}
					</p>
					<button class="main__btn mt-auto">Отправить заявку</button>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
export default {
	data: () => ({
		itemList: [
			{
				id: 0,
				title:
					'Выступление на конференциях',
				balance:
					'90 баллов',
				descr:
					'Стань спикером на международной конференции по своему направлению',
			},
			{
				id: 1,
				title:
					'Выступление на meetup',
				balance:
					'60 баллов',
				descr:
					'Стань спикером в Колёсах и на meetup других компаний. Расскажи о наших продуктах и технологиях которые мы используем',
			},
			{
				id: 2,
				title:
					'Статья на habr/vc.ru/rusbase',
				balance:
					'60 баллов',
				descr:
					'Подготовь качественный контент, напиши и опубликуй статью на	профильную тему',
			},
			{
				id: 3,
				title:
					'Мастер-классы, тренинги, лекции, подкасты, прямые эфиры',
				balance:
					'60 баллов',
				descr:
					'Поделись профессиональными знаниями с коллегами. Важно обучить не менее 6 человек',
			},
			{
				id: 4,
				title:
					'Стань ментором в проекте «Kolesa Academy»',
				balance:
					'90 баллов ежемесячно',
				descr:
					'	Стань ментором академиков, поделись своими знаниями и помоги ребятам завершить Kolesa Academy успешно',
			},
			{
				id: 5,
				title:
					'Выступление на meetup',
				balance:
					'60 баллов',
				descr:
					'	Стань спикером в Колёсах и на meetup других компаний. Расскажи о наших продуктах и технологиях которые мы используем',
			},
			{
				id: 6,
				title:
					'Помощь HR team',
				balance:
					'50 баллов',
				descr:
					'Помоги организовать мероприятие',
			},
			{
				id: 6,
				title:
					'Помощь HR team',
				balance:
					'50 баллов',
				descr:
					'Помоги организовать мероприятие',
			},
			{
				id: 7,
				title:
					'Выступление на Demoday',
				balance:
					'30 баллов',
				descr:
					'Выступи на Demoday внутри своей команды и поделись знаниями',
			},
		],
	}),
	methods: {
		goToShop() {
			this.$router.push(
				{
					name:
						'Shop',
				},
			);
		},
	},
};
</script>
<style>
</style>
