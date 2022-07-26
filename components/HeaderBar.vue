<template>
	<div class="fixed left-0 w-full mt-4">
		<div class="flex justify-between mx-4">
			<NuxtLink to="/">
				<div class="rounded-full bg-white p-2 transform hover:scale-105">
					<div v-html="$feathericons['arrow-left'].toSvg()"></div>
				</div>
			</NuxtLink>
			<!-- <div class="cursor-pointer rounded-full bg-white p-2 transform hover:scale-105" @click="openSettings">
				<div v-html="$feathericons['settings'].toSvg()"></div>
			</div> -->
		</div>
	</div>
</template>
<script>
export default {
	name: 'HeaderBar',

	methods: {
		openSettings() {

		}
	}
}
</script>
