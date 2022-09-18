<template>
	
	<div class="container">
		<SiteNavigation />
		
		<h2>{{  $route.params.slug  }}</h2>

		
	<!-- FROM ORIGINAL PAGE, UNCOMMENT IF DESIRED -->
	<!--	<h3>Filename: pages/buildings/_slug.vue</h3> -->

		<div class="building">
			<!-- the buiding returns an array with one item in it, so need to reference it below -->
			<h2>{{  building[0].title.rendered  }}</h2>

			<ul>
				<li>Address: {{  building[0].acf.location  }}</li>
				<li>Suburb: {{  building[0].acf.suburb  }}</li>
				<li>Architect: {{  building[0].acf.architect[0].name  }}</li>
			</ul>
			
			<!-- create a div to hold the renderedContent variable holding the data we've retrieved below -->
			<!-- if we don't use the v-html tag it will render it as a string -->
			<div v-html="renderedContent"></div>
			
			<!-- <pre>{{ $data }}</pre> -->
		</div>
	</div>
</template>



<script>
// in this API call, we go get a specifci building, filtered by the ID in the URL
// we access what is in the URL by using the params object
export default {
	async asyncData({ params }) {
		const building = await fetch(
			// `http://cm.beneb.com/wp-json/wp/v2/buildings/143`
			// `https://cm.beneb.com/wp-json/wp/v2/buildings/?slug=high-court-of-australia`
			`http://cm.beneb.com/wp-json/wp/v2/buildings/?slug=${params.slug}`
		).then((res) => {
			if (res.ok) {
				return res.json()
			}
			throw new Error(res.status)
		})
		return { building }

		//now we've got the data, lets create a new variable to hold just the rendered content
		let renderedContent = building[0].content.rendered;
		//return the renderedContent
		return {renderedContent}
		
	},
}
</script>




