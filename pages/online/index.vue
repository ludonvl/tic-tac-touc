<template>
	<div>
		<header-bar />
		<div class="relative flex items-top justify-center min-h-screen sm:items-center sm:pt-0">
			<div class="max-w-4xl mx-auto sm:px-6 lg:px-8">
				<board />
			</div>
		</div>
	</div>
</template>
<script>
import Pusher from 'pusher-js';

export default {
	created() {
		Pusher.logToConsole = true;

		var channel = this.pusher.subscribe('online');

		channel.bind('pusher:subscription_succeeded', (data) => {
		});

		channel.bind('pusher:member_added', (data) => {
			console.log('member_added :');
			console.log(JSON.stringify(data))
		});

		channel.bind('pusher:member_removed', (data) => {
			console.log('member_removed : '+data.info)
		});
	},

	data() {
		return {
			pusher: new Pusher('5abaa90dc6dd61fca3e0', {
				cluster: 'eu'
			}),
			messages: []
		}
	}

}
</script>
