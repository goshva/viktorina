<template>
	<div class='row justify-content-center'>
		<div class="col col-lg-4 ">
			<div class="progress">
			  <div class="progress-bar" role="progressbar" :style='questionStage'></div>
			</div>
			<div class="label-name">{{question}}</div>
			<hr>
			<div class="question-item">
				<div v-for='(item, index) in answers'>
					<input :type='answerType'
						   :key='index'
						   name='question'
						   v-model='userAnswer'
						   :value='item'
					>
					<label >{{item}}</label>
				</div>	
			</div>
			<hr>
			<button  class="btn btn-success"
			type="button"
			:class="btnClass"
			@click='userData'
			>Далее</button>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		props: ['question', 'answers', 'answerType', 'stage', 'questionsLength'],
		data() {
			return {
				userAnswer: [],

			}
		},
		computed: {
			btnClass(){
				return this.userAnswer.length ? '' : 'disabled'
			},
			questionStage () {
				let progress = (this.stage / this.questionsLength) * 100;
				return `width:${progress}%`
			}
		},
		methods: {
			userData(e) {
				if (e.target.classList.contains('disabled')) return;
				this.$emit('answer', {answer: this.userAnswer})
				this.userAnswer = [];
			}
		}
		
		
	}
	
</script>

<style scoped>
	.question-item {
		text-align: left;
	}
	
</style>