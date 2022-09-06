<template>
	<div class="container">
		<h2>All buildings</h2>
		<h3>Filename: pages/buildings/index.vue</h3>

		<SiteNavigation />


		<div class="building">
			<!-- The building list is over in the components folder -->
			<!-- the code below loads the component here so we can use it again -->
			<BuildingsList />

			<h3>new data</h3>

			<FilterBuildings />


			<!-- this is a really useful line of code that will just output what the API call returns -->
			<!-- <pre>{{ $data }}</pre> -->
		</div>
	</div>
</template>

<script>
import FilterBuildings from "../../components/FilterBuildings.vue";
// in this API call, we go get a specific building, filtered by the ID in the URL
// we access what is in the URL by using the params object
export default {
    async asyncData({ params }) {
        const building = await fetch(`http://cm.beneb.com/wp-json/wp/v2/buildings/`).then((res) => {
            if (res.ok) {
                return res.json();
            }
            throw new Error(res.status);
        });
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
        return { building };
    },
    components: { FilterBuildings }
}
</script>


<style>
</style>