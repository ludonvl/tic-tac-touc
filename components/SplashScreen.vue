<template>
	<div class="flex flex-col items-center justify-between gap-64">
		<div data-shadow="Tic Tac Toe" class="title">Tic Tac Toe</div>
		<div class="flex flex-col items-center justify-between gap-4">
			<NuxtLink to="/game">
				<button class="bg-red-500 hover:bg-red-400 text-white font-bold py-2 px-4 border-b-4 border-red-700 hover:border-red-500 rounded">
					Jouer en local
				</button>
			</NuxtLink>
			<NuxtLink to="/online">
				<button class="bg-transparent hover:bg-white hover:text-red-700 text-white font-semibold hover:text-white py-2 px-4 border border-white hover:border-transparent rounded-full">
					Jouer en ligne
				</button>
			</NuxtLink>
		</div>
	</div>
</template>
<script>
export default {
	methods: {
		solo() {
			this.$router.push('game');
		}
	}
}
</script>

<style lang="scss" scoped>
.title {
	display: inline-block;
	color: white;
	font-family: 'Pacifico', cursive;
	font-size: 5em;
	text-shadow: .03em .03em 0 hsl(358, 55%, 54%);
}
</style>
