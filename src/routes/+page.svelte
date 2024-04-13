<script>
	import { browser } from '$app/environment';
	//	import { Loader } from '@googlemaps/js-api-loader';

	// this is not really public. but since it must be used on the client,
	// it needs to be restricted via the Cloud Console (probably by domain)
	import { PUBLIC_GOOGLE_MAPS_API_KEY } from '$env/static/public';

	let map_object; // the Google Maps object
	let map_element; // the DOM element

	const initialMapDisplayOptions = {
		zoom: 8,
		center: { lat: 35, lng: -110 },
		mapId: 'SAMPLE_MAP_ID'
	};

    // "document" only exists in the browser; maps are client-side only
    if (browser) {
		((g) => { var h, a, k, p = 'The Google Maps JavaScript API', c = 'google', l = 'importLibrary', q = '__ib__', m = document, b = window; b = b[c] || (b[c] = {}); var d = b.maps || (b.maps = {}), r = new Set(), e = new URLSearchParams(), u = () => h || (h = new Promise(async (f, n) => { await (a = m.createElement('script')); e.set('libraries', [...r] + ''); for (k in g) e.set( k.replace(/[A-Z]/g, (t) => '_' + t[0].toLowerCase()), g[k] ); e.set('callback', c + '.maps.' + q); a.src = `https://maps.${c}apis.com/maps/api/js?` + e; d[q] = f; a.onerror = () => (h = n(Error(p + ' could not load.'))); a.nonce = m.querySelector('script[nonce]')?.nonce || ''; m.head.append(a); })); d[l] ? console.warn(p + ' only loads once. Ignoring:', g) : (d[l] = (f, ...n) => r.add(f) && u().then(() => d[l](f, ...n))); })
        ({
			key: PUBLIC_GOOGLE_MAPS_API_KEY,
			v: 'weekly'
		});
		map_element = document.getElementById('map');

		(async () => {
			const { Map } = await google.maps.importLibrary('maps');
			const { AdvancedMarkerElement } = await google.maps.importLibrary('marker');

			map_object = new Map(map_element, initialMapDisplayOptions);

			//const { AdvancedMarkerElement } = await loader.importLibrary('marker');
			const marker = new AdvancedMarkerElement({
				map: map_object,
				position: { lat: 0, lng: 0 },
				title: 'Greenwich'
			});
		})();
	}
</script>

<div id="map"></div>

<style>
	#map {
		height: 600px;
	}
</style>
