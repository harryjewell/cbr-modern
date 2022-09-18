<template>
	<div class="container">
		

		<SiteNavigation />

		
		<!-- FROM ORIGINAL PAGE, UNCOMMENT IF DESIRED -->
		<!-- HOME PAGE -->
	 	<h2>Home</h2> 
		<!-- <h3>Filename: pages/buildings/index.vue</h3> -->


		<div class="content index">

			<div class="homelayout">

				<div class="hometext">
					<p>Canberra Modern is an annual program of events showcasing Canberra’s unique mid and late twentieth century places and spaces.</p>
					<p>Our motto is 'Conservation Through Participation' and our innovative events aim to increase awareness of Canberra’s modernist character, heritage and uniqueness.</p>
					<p>Through event-based advocacy and engagement with the community, Canberra Modern aims to promote protection and appreciation of the places which make an irreplaceable contribution to Canberra’s 
					historic urban and designed cultural landscape.</p>
				</div>

				<img src="~assets/images/cmlogo.png" alt="" class="logohome"></img>

			</div>

		</div>
	</div>
</template>

<script>
// in this API call, we go get a specific building, filtered by the ID in the URL
// we access what is in the URL by using the params object
export default {
	async asyncData({ params }) {
		const building = await fetch(
			`http://cm.beneb.com/wp-json/wp/v2/buildings/`
		).then((res) => {
			if (res.ok) {
				return res.json()
			}
			throw new Error(res.status)
		})
		console.log(building);

		// create empty araay
		let yearArr = [];

		//loop through buildings/events array
			for (let i = 0; i < building.length; i++) {
				// some variables
				let year = "1971";
				let buildingYear = building[i].acf.year;

				// for each one, check the year
					if (buildingYear == year) {
						//if there's a match, push into new array
							yearArr.push(building[i]);
					}
			}
			console.log(yearArr);


		return { building }
	},
}
</script>


