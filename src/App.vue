<template>
	<toggle-component title="Title" @open="open">
		Test text
	</toggle-component>
</template>

<script>
import ToggleComponent from './components/ToggleComponent.vue';

export default {
	name: 'App',
	components: {
		ToggleComponent
	},
	methods: {
		open(value) {
			console.log(value);
		}
	}
};
</script>

<style>
#app {
	margin-top: 60px;
}
</style>
