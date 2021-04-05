<template>
  <div class="markdown-body">
		<div  v-if="postInMarkdown.length > 0">
			<h2>{{ postInMarkdown.title }}</h2>
			<h3>by  {{ postInMarkdown.author }}</h3>
			<nuxt-content :document="postInMarkdown"></nuxt-content>
		</div>
		<div v-else>
			<p>Nothing to see here, check back once in a while to see if there is a post.</p>

		</div>
  </div>

</template>

<script>
  export default {
    async asyncData({$content, params}) {
      const postInMarkdown = await $content(params.slug)
        .fetch()
        .catch(err => console.log(err))
      console.log(postInMarkdown)
      return {
        postInMarkdown
      }
    }
  }
</script>

<style>
.markdown-body {
		box-sizing: border-box;
		min-width: 200px;
		max-width: 980px;
		margin: 0 auto;
		padding: 45px;
	}

	@media (max-width: 767px) {
		.markdown-body {
			padding: 15px;
		}
	}
</style>
