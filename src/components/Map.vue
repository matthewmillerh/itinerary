<script>
    import mapboxgl from 'mapbox-gl'
    mapboxgl.accessToken = "pk.eyJ1IjoibWF0dGhld21pbGxlcmgiLCJhIjoiY20wdXZ0cGYxMTlmZTJpczVpdXExOXdkYyJ9.kKG0mzGlM_tEJt-FLVhuCQ"

    export default{
        mounted() {
            const map = new mapboxgl.Map({
            container: this.$refs.mapContainer,
            style: "mapbox://styles/mapbox/streets-v12", // Replace with your preferred map style
            center: [2.3514, 48.8575],
            zoom: 9,
            });

        this.map = map;
        },
        unmounted() {
            this.map.remove()
            this.map = null
        }
    }
    
    
</script>
<template>
    <div ref="mapContainer" class="map-container w-auto h-96 rounded-lg"></div>
</template>
<style></style>