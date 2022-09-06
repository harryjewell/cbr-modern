<!-- this component returns a list of all the buildings -->
<template>
	<div class="">
		<!-- these would show while the data loads or if an error -->
		<p v-if="$fetchState.pending">Loading buildings...</p>
		<p v-else-if="$fetchState.error">Error while fetching buildings</p>

		<ul v-else class="list-group">
			<!-- this is a for loop, it just loops through the list of buildings returned from the API -->
			<li v-for="building in buildings" :key="building.id" class="list-group-item">
				<!-- now make a link for each item -->
				<!-- <NuxtLink :to="building.slug"> -->
				<NuxtLink :to="'/buildings/' + building.slug">
					<!-- return the rendered title -->
					{{  building.title.rendered  }}
				</NuxtLink>
				<!-- now show me the building year -->
				: {{ building.acf.year }}
			</li>
		</ul>

	</div>
</template>


<script>



export default {

	async fetch() {
		this.buildings = await fetch('http://cm.beneb.com/wp-json/wp/v2/buildings/?per_page=20')
		.then((res) =>
			res.json()
		)
	},
	data() {

		// // create empty araay
		// let yearArr = [];

		// //loop through buildings/events array
		// 	for (let i = 0; i < building.length; i++) {
		// 		// some variables
		// 		let year = "1971";
		// 		let buildingYear = building[i].acf.year;

		// 		// for each one, check the year
		// 			if (buildingYear == year) {
		// 				//if there's a match, push into new array
		// 					yearArr.push(building[i]);
		// 			}
		// 	}
		// 	console.log(yearArr);

		return {
			buildings: [],
		}
	},


	// async asyncData({ params }) {
	// 	const building = await fetch(
	// 		`http://cm.beneb.com/wp-json/wp/v2/buildings/`
	// 	).then((res) => {
	// 		if (res.ok) {
	// 			return res.json()
	// 		}
	// 		throw new Error(res.status)
	// 	})
	// 	console.log(building);

	// 	// create empty araay
	// 	let yearArr = [];

	// 	//loop through buildings/events array
	// 		for (let i = 0; i < building.length; i++) {
	// 			// some variables
	// 			let year = "1971";
	// 			let buildingYear = building[i].acf.year;

	// 			// for each one, check the year
	// 				if (buildingYear == year) {
	// 					//if there's a match, push into new array
	// 						yearArr.push(building[i]);
	// 				}
	// 		}
	// 		console.log(yearArr);


	// 	return { building }
	// },
}
</script>