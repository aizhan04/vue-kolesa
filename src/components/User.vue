<template>
	<a href="/" class="user_info">
		<div class="user_info__wrapper">
			<div>
				<img class="user_info__photo" :src="user.avatarUrl" alt="photo" />
			</div>
			<nav class="user_info__menu">
				<ul>
					<li>
						<a href="#" class="user_info__title">{{ user.name }}</a>
					</li>
					<li>
						<a href="#" class="user_info__balance">{{ user.score }}</a>
					</li>
				</ul>
			</nav>
		</div>
	</a>
</template>

<script>
export default {
	name:
		'User',
	props: {
		user: Object,
	},
};
</script>
