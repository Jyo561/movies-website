<template>
	<div class="movie-detail">
		<h2>{{ movie.Title }}</h2>
		<p>{{ movie.Year }}</p>
		<img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
		<br>
		<h4 class="linew">Rated:{{ movie.Rated }}</h4>
		<h3 class="linew" style="margin-left:20px">Rating:{{ movie.imdbRating }}</h3>
		<p>{{ movie.Plot }}</p>
	</div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
	setup () {
		const movie = ref({});
		const route =useRoute();

		onBeforeMount(() => {
				fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
					.then(response => response.json())
					.then(data => {
						movie.value = data;
					})
		});

		return {
			movie
		}
	}
}
</script>

<style lang="scss">
.movie-detail{
	padding: 16px;
  align-items: center;
	h2{
		color: #E0FFFF;
		font-size: 28px;
		font-weight:600;
		margin-bottom: 16px;
	}
	p{
		color: #FFF;
		font-size: 16px;
		line-height: 1.4;
	}

	.linew{
		display: inline;
		color: #FFF;
	}
}
</style>
