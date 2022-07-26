<template>
	<div class="rounded-full shadow-2xl bg-white">
		<progress-circle :completed-steps="currentTimer"
			:total-steps="maxTime"
			:diameter="40"
			:circle-width="3"
			:circle-color="'#eee'"
			:start-color="'green'"
			:stop-color="'red'"
		>
			<span class="font-bold text-s">{{ currentTimer }}</span>
		</progress-circle>
	</div>
</template>
<script>
import { ProgressCircle } from 'vue-progress-circle'

export default {
	components: {
		ProgressCircle
	},

	props: {
		maxTime: {
			type: Number,
			default: 60
		}
	},

	methods: {
		stop() {
			this.currentTimer = 0;

			if (this.timer) {
				clearInterval(this.timer);
			}
		},

		start() {
			this.timer = setInterval(() => {
				this.currentTimer++;
				if (this.currentTimer > this.maxTime) {
					this.currentTimer = 0;
					this.$emit('expired-timer');
				}
			}, 1000);
		},

		restart() {
			this.stop();
			this.start();
		},
	},

	data() {
		return {
			currentTimer: 0,
			timer: null,
		}
	}
}
</script>
