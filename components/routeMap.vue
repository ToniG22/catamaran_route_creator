<template>
    <div class="flex flex-col gap-5">
        <div class="flex flex-row justify-center items-center">
            <h1 class="text-black text-2xl">Catamaran Route Creator</h1>
        </div>
        <div ref="mapContainer" style="height: 72vh; width: 72vw">
            <LMap ref="mapRef" :zoom="13" :center="center" :use-global-leaflet="false" @click="handleMapClick">
                <LTileLayer url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
                    attribution="&copy; OpenStreetMap contributors" />
                <LMarker v-for="(point, index) in trajectory" :key="index" :lat-lng="[point.lat, point.lng]" />
                <LPolyline v-if="trajectory.length > 1" :lat-lngs="trajectory.map(p => [p.lat, p.lng])" :weight="4"
                    color="blue" />
            </LMap>
        </div>

        <div class="flex flex-row justify-between">
            <UButton class="shadow-gray-600 shadow text-black" color="error" size="xl" icon="mdi-light-cancel"
                @click="clearTrajectory">
                Clear Trajectory
            </UButton>

            <UButton class="shadow-gray-600 shadow text-black" :color="enableDrawing ? 'warning' : 'secondary'"
                size="xl" :icon="enableDrawing ? 'mdi-light-stop' : 'mdi-light-map-marker'" @click="toggleDrawing">
                {{ enableDrawing ? 'Stop Drawing' : 'Draw Trajectory' }}
            </UButton>

            <UButton class="shadow-gray-600 shadow text-black" color="success" size="xl" icon="mdi-light-download"
                @click="exportToCSV">
                Export Trajectory (CSV)
            </UButton>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import { LMap, LTileLayer, LMarker, LPolyline } from '@vue-leaflet/vue-leaflet'

// State
const center = ref([32.6423552, -16.9067382])
const trajectory = ref([])
const enableDrawing = ref(false)

// Refs
const mapContainer = ref(null)

// Handle map click
const handleMapClick = (event) => {
    if (!enableDrawing.value) return
    const { latlng } = event
    trajectory.value.push({
        lat: latlng.lat,
        lng: latlng.lng
    })
}

// Toggle drawing mode
const toggleDrawing = () => {
    enableDrawing.value = !enableDrawing.value
}

// Clear trajectory
const clearTrajectory = () => {
    trajectory.value = []
    enableDrawing.value = false
}

// Export to CSV
const exportToCSV = () => {
    if (trajectory.value.length === 0) return

    const csvRows = ['index,lat,lng']
    trajectory.value.forEach((point, index) => {
        csvRows.push(`${index},${point.lat},${point.lng}`)
    })

    const csvContent = csvRows.join('\n')
    const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' })
    const url = URL.createObjectURL(blob)
    const link = document.createElement('a')
    link.setAttribute('href', url)
    link.setAttribute('download', 'trajectory.csv')
    link.style.visibility = 'hidden'
    document.body.appendChild(link)
    link.click()
    document.body.removeChild(link)
}
</script>