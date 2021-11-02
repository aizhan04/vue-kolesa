<template>
	<a href="/" class="user_info">
		<div class="user_info__wrapper">
			<div>
				<img class="user_info__photo" :src="userInfo.avatarUrl" alt="photo" />
			</div>
			<nav class="user_info__menu">
				<ul>
					<li>
						<a href="#" class="user_info__title">{{ userInfo.name }}</a>
					</li>
					<li>
						<a href="#" class="user_info__balance">{{ userInfo.score }}</a>
					</li>
				</ul>
			</nav>
		</div>
	</a>
</template>

<script>
import { mapState } from 'vuex';

export default {
	name:
		'User',
	computed: {
		...mapState(
			{
				userInfo:
					'userInfo',
			},
		),
	},
	mounted() {
		this.fetchUser();
	},
	methods: {
		fetchUser() {
			this.$store.dispatch(
				'fetchUserInfo',
			);
		},
	},
};
</script>
