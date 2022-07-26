<template>
	<div class="flex flex-col gap-9">
		<Player :name="secondPlayerName" :shape="secondPlayerShape" :win="secondPlayerWin" :has-to-play="isSecondPlayerToPlay" :is-reversed="true" />
		<div class="bg-white overflow-hidden border-none shadow-xl sm:rounded-lg p-6">
			<div class="game">
				<div v-for="cell in squareCells" :key="cell" class="game-cell" @click="setChoice(cell)">
					<img v-show="choices[cell] === 1" width="32" src="circle.png" />
					<img v-show="choices[cell] === 2" width="32" src="cross.png" />
				</div>
			</div>
			<Winner v-if="currentWinner" :name="currentWinner.name" :shape="currentWinner.shape" />
		</div>
		<Player :name="firstPlayerName" :shape="firstPlayerShape" :win="firstPlayerWin" :has-to-play="isFirstPlayerToPlay" />
		<div class="flex items-center justify-between">
			<div>
				<button @click="restart" class="inline-flex items-center bg-[#F78317] hover:bg-red-400 text-white font-bold py-2 px-4 border-b-4 border-red-700 hover:border-red-500 rounded">
					<div v-html="$feathericons['repeat'].toSvg()" class="mr-2"></div>
					<div>Recommencer</div>
				</button>
			</div>
			<Timer ref="timer" @expired-timer="changePlayer" />
		</div>
	</div>
</template>
<script>
export default {
	computed: {
		isFirstPlayerToPlay() {
			if (this.players.length > 0 && 'id' in this.players[0]) {
				return this.currentPlayer === this.players[0].id;
			}

			return false;
		},

		firstPlayerName() {
			if (this.players.length > 0 && 'name' in this.players[0]) {
				return this.players[0].name;
			}

			return '';
		},

		firstPlayerShape() {
			if (this.players.length > 0 && 'shape' in this.players[0]) {
				return this.players[0].shape;
			}

			return '';
		},

		firstPlayerWin() {
			if (this.players.length > 0 && 'win' in this.players[0]) {
				return this.players[0].win;
			}

			return 0;
		},

		isSecondPlayerToPlay() {
			if (this.players.length > 1 && 'id' in this.players[1]) {
				return this.currentPlayer === this.players[1].id;
			}

			return false;
		},

		secondPlayerName() {
			if (this.players.length > 1 && 'name' in this.players[1]) {
				return this.players[1].name;
			}

			return '';

		},

		secondPlayerShape() {
			if (this.players.length > 1 && 'shape' in this.players[1]) {
				return this.players[1].shape;
			}

			return '';

		},

		secondPlayerWin() {
			if (this.players.length > 1 && 'win' in this.players[1]) {
				return this.players[1].win;
			}

			return 0;
		},
	},

	methods: {
		changePlayer() {
			this.currentPlayer = this.currentPlayer === 1 ? 2 : 1;
		},

		setChoice(index) {
			if (!this.currentWinner && this.choices[index] === 0) {
				this.choices[index] = this.currentPlayer;
				this.checkEnd();
				if (!this.currentWinner) {
					this.$refs.timer.restart();
					this.changePlayer();
				}
			}
		},

		setGame() {
			this.currentPlayer = this.defaultPlayer;
			this.currentWinner = null;
			for (let index = 1; index <= this.squareCells; index++) {
				this.$set(this.choices, index, 0);
			}
		},

		checkEnd() {
			this.players.every(player => {
				if (this.checkWin(player.id)) {
					this.winner(player);
					this.$refs.timer.stop();
					return false;
				}
				return true;
			});

			this.checkTie();
		},

		checkWin(player) {
			return (this.choices[1] === player && this.choices[2] === player && this.choices[3] === player)
				|| (this.choices[4] === player && this.choices[5] === player && this.choices[6] === player)
				|| (this.choices[7] === player && this.choices[8] === player && this.choices[9] === player)
				|| (this.choices[1] === player && this.choices[4] === player && this.choices[7] === player)
				|| (this.choices[2] === player && this.choices[5] === player && this.choices[8] === player)
				|| (this.choices[3] === player && this.choices[6] === player && this.choices[9] === player)
				|| (this.choices[1] === player && this.choices[5] === player && this.choices[9] === player)
				|| (this.choices[3] === player && this.choices[5] === player && this.choices[7] === player)
		},

		checkTie() {
			return ;
		},

		winner(player) {
			this.currentWinner = player;
			player.win++;
		},

		restart() {
			this.setGame();
			this.$refs.timer.stop();
		}
	},

	created() {
		this.setGame();
	},

	data() {
		return {
			defaultPlayer: 1,
			currentPlayer: 1,
			currentWinner: null,
			currentTimer: 0,
			players: [
				{
					id: 1,
					name: 'Joueur 1',
					win: 0,
					shape: 'circle.png'
				},
				{
					id: 2,
					name: 'Joueur 2',
					win: 0,
					shape: 'cross.png'
				}
			],
			squareCells: 9,
			choices: {},
		}
	}
}
</script>
<style lang="scss" scoped>
.game {
    display: grid;
    grid-template-columns: repeat(3, auto);
    width: 306px;
    margin: 10px auto;

	&-cell {
		width: 100px;
		height: 100px;
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;

		&:nth-of-type(1) {
			border-bottom: 2px solid #eee;
			border-right: 2px solid #eee;
		}

		&:nth-of-type(2) {
			border-bottom: 2px solid #eee;
		}

		&:nth-of-type(3) {
			border-left: 2px solid #eee;
			border-bottom: 2px solid #eee;
		}

		&:nth-of-type(4) {
			border-right: 2px solid #eee;
		}

		&:nth-of-type(6) {
			border-left: 2px solid #eee;
		}

		&:nth-of-type(7) {
			border-top: 2px solid #eee;
			border-right: 2px solid #eee;
		}

		&:nth-of-type(8) {
			border-top: 2px solid #eee;
		}

		&:nth-of-type(9) {
			border-top: 2px solid #eee;
			border-left: 2px solid #eee;
		}
	}
}
</style>
