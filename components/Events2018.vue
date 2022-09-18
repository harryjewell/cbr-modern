<!-- this component returns a list of all the events by year -->
<template>
	<div class="content">
		<!-- these would show while the data loads or if an error -->
		<p v-if="$fetchState.pending"> <span class="loading"></span></p>
		<p v-else-if="$fetchState.error">Error while fetching events</p>

		<ul v-else class="list-group">
			<!-- this is a for loop, it just loops through the list of events returned from the API -->
			<li v-for="event in events" :key="event.id" class="list-group-item">
				<!-- now make a link for each item -->
				<!-- <NuxtLink :to="event.slug"> -->
				<NuxtLink :to="'/events/' + event.slug">
					<!-- return the rendered title -->
					{{  event.title.rendered  }}
				</NuxtLink>
				<!-- now show me the event year -->
				: {{ event.acf.year }}
			</li>
		</ul>

	</div>
</template>


<script>
export default {
	//data will return an array
	data() {
		return {
			//empty array to be filled
			events: [],
		}
	},
	//now go get the data
	async fetch() {
		//make the api call and fill the empty events array
		let apiData = await fetch('http://cm.beneb.com/wp-json/wp/v2/events/?per_page=100')
		.then((response) =>
			response.json()
		)
		// // create empty araay
		let yearArr = [];
		//loop through events/events array
		for (let i = 0; i < apiData.length; i++) {
			// some variables
			let year = "2018";
			let eventYear = apiData[i].acf.year;
			// for each one, check the year
				if (eventYear == year) {
					//if there's a match, push into new array
						yearArr.push(apiData[i]);
				}
		} 
		//now set events to be the yearArray 
		this.events = yearArr;
	},
	
	
}
</script>