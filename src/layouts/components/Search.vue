<template>
	<div>
		<form class="section_header_wrapper__search_block">
			<input
				class="search_input"
				type="text"
				placeholder="Поиск"
				name="search"
				:value="modelValue"
				@input="$emit('update:modelValue', $event.target.value)"
			/>
			<img class="search_icon" src="@/assets/search_icon.svg" alt="search" />
		</form>
	</div>
</template>

<script>
export default {
	name:
		'Search',
	props: {
		modelValue: String,
	},
};
</script>
