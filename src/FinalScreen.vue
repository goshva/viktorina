<template>
	<div>
		<div class="row">
			<div class='col'>
				<div class="progress">
				  <div class="progress-bar" role="progressbar" :style='progressWidth'>
				  	
				  </div>
				</div>
				{{howManyCorrect}}
				<hr>
				<div v-for='(item,i) in questions'
				>
					<div class="row" :class='questionClass(i)' :key='i'>
						<div class="col">{{item.question}}</div>
						<div class="col">Ваш ответ: {{item.userAnswer}}</div>
						<div class="col">Правильный ответ: {{item.correctAnswer}}</div>
						{{i}}
					</div>
				</div>
			</div>
		</div>
		<div class="row">
			<div class="col">
				<button class="btn btn-success"
					@click='again'
				>Заново</button>
			</div>
		</div>	
	</div>
</template>

<script>
	export default {
		props: ['questions'],
		data() {
			return {
				isCorrectClass: [],


			}
		},
		computed: {
			progressWidth(){
				let correct = 0;
				let width = 0;
				let that = this;
				this.questions.forEach( (item, index) => {
					if (that.arraysEqual(item.correctAnswer,item.userAnswer )) {
						correct++;
						this.isCorrectClass[index] = true
					} else this.isCorrectClass[index] = false
				})
				width = (correct / this.questions.length ) *100;
				return `width:${width}%`
			},
			howManyCorrect() {
				let correct = 0;
				this.isCorrectClass.forEach( (item) => {
					item ? correct++ : '';
				})
				return `Вы ответили правильно на ${correct} из ${this.isCorrectClass.length} вопросов`;
			}


		},
		methods: {
			questionClass(i) {
				return this.isCorrectClass[i] ? 'text-success' : 'text-danger'
			},
			again() {
				this.$emit('again');
			}

		},
		
		
	}	
</script>

<style>
	
</style>