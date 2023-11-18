<template>
	<div class="tag__list" :class="{ 'align-width': alignment === 'width' }">

			<!-- проходимся по всему массиву из всех элементов -->
			<section class="tags__wrapper-item" v-for="index in range" :key="index">
				
				<!-- если число не even то определяем что это текст и дальше по условию работаем с этим объектом  -->
				<template v-if=" !(index % 2) "> 
					<v-btn class="tag" icon>

					<!-- в массиве tags определяем какой сейчас истинный индекс и с помощью этого определяем какой по счету индекс для тега -->
					<v-icon :class="{ 'tags__icon-margin-left' : tags[supportArrayFindOut[index].currentNum] && tags[supportArrayFindOut[index].currentNum].icon }">{{ tags[supportArrayFindOut[index].currentNum] && tags[supportArrayFindOut[index].currentNum].icon }}</v-icon>
						<span v-if="index === 0">{{tags[index].text }}</span>
						<span v-else>{{tags[supportArrayFindOut[index].currentNum] && tags[supportArrayFindOut[index].currentNum].text }}</span>
					</v-btn>
				</template>

				<!-- если число even то это точка и вместо текста по условию генерируем компонент точки -->
				<template v-else>
					<v-icon class="tag__dot-target" >mdi-circle-small</v-icon>
				</template>
			</section>
		</div>
	</template>
 <script>
 export default {
	props: {
		tags: {
			type: Array,
			required: true,
		},
		icon: {
			type: String,
			default: "default-icon",
		},
		alignment: {
			type: String,
			default: "left",
		},
	},
	computed: {
		range() {
			//Массив со всеми элементами (точки, теги)
			return Array.from({ length: this.tags.length * 2 - 1 }, (_, index) => index)
		},
		filteredTags() {
			//Массив тегов для удобного доступа к тексту тега и иконке
			return this.tags
		},
		supportArrayFindOut() {
			const supportArray = []
			
			//currentNum определяет индекс числа even
			let currentNum = 0

			//цикл для всех элементов (точек и тегов)
			for (let i = 0; i <= this.tags.length * 2 - 1; i++) {
				
				//условие определяет где будут точки и добавляет пустой объект (можно улучшить) 
				if(i % 2) {
					supportArray.push({})
					continue
				}  
				//добавляет истинный индекс числа even
				supportArray.push({currentNum})

				//инкрементирую число чтобы потом добавить следующий индекс числа even
				currentNum++	
			}
			return supportArray
		}
	},
 }
 </script>
 
 <style scoped lang="scss">
 .dots__wrapper {
	display: flex;
 }
 .tags__icon-margin-left {
	margin-left: 24px !important;
 }
 .tag__list {
	display: flex;
	flex-wrap: wrap;
	justify-content: left;
	align-items: center;
}
.tag__dot-target{
	flex-grow: 1 !important;
}
 .align-width {
	justify-content: space-between;
 }
 .tag {
	width: auto !important;
	&:last-child {
		margin-right: 24px;
	}
 }

 @media screen and (max-width: 550px) {
		span {
			font-size: 10px;
		}
	}
 </style>