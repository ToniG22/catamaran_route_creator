# 🗺️ Nuxt Catamaran Trajectory Drawer

An interactive map-based application built with **Nuxt** and **NuxtLeaflet** that allows users to draw GPS trajectories, view them as connected points, clear them, and export the data as a CSV file.

---

## ✨ Features

- 🖱️ **Draw Trajectory**: Toggle drawing mode and click on the map to place points.
- 📍 **Connected Points**: Automatically connects placed points with a polyline.
- 🧹 **Clear Trajectory**: Remove all placed points with one click.
- 📤 **Export to CSV**: Download the trajectory data (`lat`, `lon`, `index`) in CSV format.

---

## 📁 Project Structure

```
src/
├── components/
│   └── routeMap.vue      # Main component with map + trajectory logic
├── pages/
│   └── index.vue      # Main page
├── App.vue
```

---

## 🛠 Tech Stack

- [Nuxt](https://nuxt.com/)
- [NuxtLeaflet](https://leaflet.nuxtjs.org/)
- [OpenStreetMap Tiles](https://www.openstreetmap.org/)

---

## 🚀 Getting Started

### Installation

1. Clone the repo:

```bash
git clone https://github.com/ToniG22/catamaran_route_creator.git
cd catamaran_route_creator
```

2. Install dependencies:

```bash
npm install
```

3. Start the development server:

```bash
npm run dev
```

Open your browser at `http://localhost:3000` (or the port provided).

---

## 📄 License

TBD