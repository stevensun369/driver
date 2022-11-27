<script>

	import axios from 'axios'

	import {writable} from 'svelte/store'

	let lat = writable("")
	let long = writable("")
	let loaded = writable("")

	function success (pos) {
		$lat = pos.coords.latitude;
		$long = pos.coords.longitude;

		console.log($lat + " " + $long)
	}

	setInterval(async () => {
		navigator.geolocation.getCurrentPosition(success)

		try {
			const {data} = await axios.get(
				`https://api.elmtree.ro/send?long=${$long}&lat=${$lat}`
			)
			// alert($lat + " " + $long)

			$loaded = true
		} catch (error) {
			console.log(error)
		}
	}, 1000)


</script>