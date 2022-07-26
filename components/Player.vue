<template>
	<div class="flex justify-between items-center" :class="{'flex-row-reverse': isReversed}">
		<div>
			<div>
				{{ image }}
			</div>
			<div class="flex items-center gap-1 text-white">
				<div v-show="hasToPlay" class="rounded-full w-1 h-1 bg-white"></div>
				<div class="font-bold text-s">{{ name }}</div>
				<img class="player-shape grayscale hover:cursor-pointer hover:grayscale-0" :src="shape" />
			</div>
		</div>
		<div class="rounded-full bg-white py-1 w-10 drop-shadow-2xl border-none flex justify-center items-center font-bold text-s" v-if="win >= 0">
			{{ win }}
		</div>
	</div>
</template>
<script>
export default {
	name: 'Player',

	props: {
		name: {
			type: String,
			required: true,
		},
		image: {
			type: String,
			default: () => { return ''; }
		},
		shape: {
			type: String,
			required: true
		},
		win: {
			type: Number,
			required: false
		},
		hasToPlay: {
			type: Boolean,
			required: true,
		},
		isReversed: {
			type: Boolean,
			default: false
		}
	}
}
</script>
<style lang="scss" scoped>
.player {
	&-shape {
		width: 12px;
		height: 12px;
	}
}
</style>
