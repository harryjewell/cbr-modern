<template>
	<div class="container">
		<SiteNavigation />

		<h2>{{ $route.params.slug }}</h2>

		<h2>About</h2>
		<!-- <h3>Filename: pages/_pages.vue</h3> -->

		<div class="page">
			<!-- the buiding returns an array with one item in it, so need to reference it below -->
			<!-- <h2>{{  page[0].title.rendered  }}</h2> -->

			<!-- create a div to hold the renderedContent variable holding the data we've retrieved below -->
			<!-- if we don't use the v-html tag it will render it as a string -->
			<div v-html="renderedContent"></div>
			<pre>{{ $data }}</pre>
		</div>
	</div>
</template>

<script>
// in this API call, we load a page based off the URL paramter
// we access what is in the URL by using the params object
export default {
	async asyncData({ params }) {
		const page = await fetch(
			// `http://cm.beneb.com/wp-json/wp/v2/pages/?slug=${params.slug}`
			// `http://cm.beneb.com/wp-json/wp/v2/pages/157`
			`http://cm.beneb.com/wp-json/wp/v2/pages/?slug=about`
		).then((res) => {
			if (res.ok) {
				return res.json()
			}
			throw new Error(res.status)
		})
		//now we've got the data, lets create a new variable to hold just the rendered content
		let renderedContent = page[0].content.rendered;
		//return the renderedContent
		return {renderedContent}
		
		//return all page data
		return { page }
	},
}
</script>
