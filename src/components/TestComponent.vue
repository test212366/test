<template>
	<div id="app">
		<section class="test__wrapper">
			<tags-list :tags="tags1" alignment="left"/>
			<tags-list :tags="tags2" alignment="width"/>
			<section class="test__wrapper-50percent">
				<tags-list :tags="tags3" alignment="left"/>
			</section>
			<section class="test__wrapper-50percent">
				<tags-list :tags="tags4" alignment="width"/>
			</section>
		</section>
	</div>
 </template>
 
 <script>
 import TagsList from "./TagsComponent"
 export default {
	components: {
	TagsList,
	},
	data() {
		return {
			tags1: [
				{ text: "text1", icon: "mdi-flag" },
				{ text: "text1" },
				{ text: "text1", icon: "mdi-heart"},
				{ text: "text2", icon: "mdi-heart"},
			],
			tags2: [
				{ text: "text1" },
				{ text: "text2", icon: "mdi-heart" },
			],
			tags3: [
				{ text: "text1" },
				{ text: "text2", icon: "mdi-heart" },
			],
			tags4: [
				{ text: "text1" },
				{ text: "text2", icon: "mdi-flag" },
			],
		}
	},
 }
 </script>
 
 <style lang="scss">
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
	.test__wrapper {
		display: flex;	
		flex-direction: column;
		width: 100%;
		&-50percent {
			max-width: 50%;
		}
	}

	@media screen and (max-width: 550px) {
		.test__wrapper-50percent {
			max-width: 100%;
		}
	}

 </style>
 