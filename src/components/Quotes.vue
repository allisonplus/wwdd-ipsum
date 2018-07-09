<template>
	<div class="quote">
		<p class="quote-content">{{quote}}</p>
	<button @click="getRandomQuote" class="button">Get More Sparkle</button>
	</div>
</template>

<script>
	import {quotes} from '../quotes.json';

	export default {
		name: 'quote',
		props: [ 'getRandomNumber', 'getRandomColour' ],
		data: function() {
			return {
				quote: "",
			}
		},
		methods: {
			getRandomQuote: function() {
				let index = this.getRandomNumber(quotes);
				this.quote = `"${quotes[index]}"`;
				this.getRandomColour();
			},
		},
		mounted: function() {
			this.getRandomQuote();
		},
	}
</script>

<style lang="scss">
@import '../assets/styles/_global.scss';

	.quote {
		position: relative;

		.quote-content {
			font-family: $serif;
			font-size: 28px;
			letter-spacing: 1.6px;
			margin-top: 0;

			@media (min-width: $tablet-portrait) {
				font-size: 34px;
				min-height: 175px;
			}
		}
	} // .quote
</style>
