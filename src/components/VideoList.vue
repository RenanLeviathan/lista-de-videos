<script setup>
import { getVideos } from '../services/videos.js'
import { ref, computed } from 'vue'
import YoutubeIframe from '@/components/YoutubeIframe.vue'
const source = ref("")

//paginador
const currentPage = ref(1)

const pageSize = ref(3)

const videosList = computed(() => getVideos())

const totalPages = computed(() => 
  Math.ceil(videosList.value.length / pageSize.value)
)
console.log(totalPages.value)

const pages = computed(() => {
	const startIndex = (currentPage.value - 1) * pageSize.value
	const endIndex = startIndex + pageSize.value
	
	return videosList.value.slice(startIndex, endIndex)
})

const pageNumbers = computed(()=>{
  return Array.from({ length: totalPages.value }, (_, i) => i + 1);
})

function change(p) {
  currentPage.value = p
}
</script>
<template>
<div class="wrapper">
	<nav>
		<a v-for="v in pages" href="#" @click="source = v.href">{{v.title}}</a>
		<!-- <video :src="v.href">This browser does not support HTML5</video> -->
	</nav>
	<div class="video-container">
		<YoutubeIframe v-if="source" :src="source"/>
	</div>
	<span v-if="!source">Selecione um vídeo na lista</span>
</div>
<div class="wrapper">
	<div class="pager">
		<a href="#" v-for="p in pageNumbers" @click="change(p)" class="page-items" :class="currentPage == p ? 'activated' : ''">{{ p }}</a>
	</div>
</div>
</template>
<style scoped>
	.wrapper{
		display: flex;
		justify-content: flex-start;
	}
	
	.wrapper nav{
		min-height: 300px;
	}

	.pager{
		display: flex;
		justify-content: space-evenly;
	}

	.page-items{
		padding: 5px;
		text-decoration: none;
		background: #8cbfbf;
		color: #1e3b3b;
	}

	.activated{
		padding: 5px;
		text-decoration: none;
		background: #1e3b3b;
		color: #8cbfbf;
	}

	nav{
		width: 100%;
		height: auto;
	}

	nav a{
		display: block;
		width: 200px;
		text-decoration: none;
		background-color: #bfe7e7;
		padding: 3px;
		color: #000;
	}

	nav a:hover{
		background-color: #8cbfbf;
	}

	.video-container, span{
		display: flex;
	}
</style>