<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="utf-8" />
    <title>Poltava Tactical Radar v6.0</title>
    <script src="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.js"></script>
    <link href="https://unpkg.com/maplibre-gl@latest/dist/maplibre-gl.css" rel="stylesheet" />
    <style>
        body { margin: 0; padding: 0; background: #000; overflow: hidden; font-family: monospace; }
        #map { position: absolute; top: 0; bottom: 0; width: 100%; }
        .ui-overlay {
            position: absolute; top: 15px; left: 15px; z-index: 10;
            background: rgba(0, 0, 0, 0.9); color: #00ff00;
            padding: 15px; border-radius: 10px; border: 1px solid #00ff00;
            pointer-events: none; min-width: 150px;
        }
        .marker-wrapper { position: relative; width: 0; height: 0; display: flex; align-items: center; justify-content: center; }
        .icon-base { width: 36px; height: 36px; background-size: contain; background-repeat: no-repeat; }
        .drone-label { 
            position: absolute; left: 22px; background: rgba(0,0,0,0.85); 
            color: #00ff00; font-size: 10px; padding: 2px 6px; 
            border: 1px solid #00ff00; border-radius: 4px; white-space: nowrap; 
        }
        .label-red { color: #ff4444; border-color: #ff4444; font-weight: bold; }
        /* Иконки */
        .geran-icon { background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 600.51 600.51'%3E%3Cpath fill='none' stroke='%2300ff00' stroke-width='20' d='M555.25,562.35l-111.64-153.95c-.23-7.93,0-12.69,0-12.69l-100.51-138.6v-65.98c-1.83-92.34-30.42-88.48-30.42-88.48s-28.59-3.86-30.42,88.48v65.98l-99.41,137.09-110.84,152.85s-3.14,5.49.99,44.59l12.8-12.85h103.11s.2-27.98.2-27.98h103.11s.2,27.98.2,27.98h103.11l12.8,12.85Z'/%3E%3C/svg%3E"); }
        .rocket-icon { background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 1049.1 1049.1'%3E%3Cpath fill='none' stroke='red' stroke-width='30' d='M504.8,62.6c-7.4,20.9-14.5,51.5-16.2,94.2-3.3,38.7-12.8,152.7-19.7,241.7l-1.4,19.4v382.7l-8.1,19v41.8l15.7-5.4h20.4v14.9h16.4l15.7,5.4v-41.8l-8-18.6v-366.4c-6.9-89-16.5-203.1-19.7-241.7-1.7-42.7-8.8-73.3-16.2-94.2Z'/%3E%3C/svg%3E"); }
    </style>
</head>
<body>

<div class="ui-overlay">
    <div id="clock" style="font-size: 22px; font-weight: bold;">00:00:00</div>
    <div style="font-size: 10px; color: #888; margin-bottom: 5px;">FIREBASE CLOUD ACTIVE</div>
    <div style="color: #ff4444; border-top: 1px solid #333; padding-top: 5px;">ЦІЛЕЙ: <span id="count">0</span></div>
</div>

<div id="map"></div>

<script type="module">
    // Инициализация Firebase с твоими данными
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
    import { getDatabase, ref, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

    const firebaseConfig = {
        apiKey: "AIzaSyDQuG3bhnmBBAAPSFBNK5KvfWiNYQogYxI",
        authDomain: "poltava-radar-e7c7b.firebaseapp.com",
        databaseURL: "https://poltava-radar-e7c7b-default-rtdb.europe-west1.firebasedatabase.app",
        projectId: "poltava-radar-e7c7b",
        storageBucket: "poltava-radar-e7c7b.firebasestorage.app",
        messagingSenderId: "462672460900",
        appId: "1:462672460900:web:e2fc681485fae56944b371",
        measurementId: "G-7LSFD0GMNP"
    };

    const app = initializeApp(firebaseConfig);
    const db = getDatabase(app);
    const targetsRef = ref(db, 'targets');

    const map = new maplibregl.Map({
        container: 'map',
        style: 'https://basemaps.cartocdn.com/gl/dark-matter-gl-style/style.json',
        center: [34.55, 49.59],
        zoom: 8
    });

    const drones = {};

    // Функция отрисовки цели
    function drawTarget(id, data) {
        if (drones[id]) drones[id].marker.remove();

        const wrapper = document.createElement('div');
        wrapper.className = 'marker-wrapper';
        const isRocket = data.type.includes('РАКЕТА') || data.type.includes('БАЛІСТИКА');
        
        const ico = document.createElement('div');
        ico.className = isRocket ? 'icon-base rocket-icon' : 'icon-base geran-icon';
        ico.style.transform = `rotate(${data.angle}deg)`;
        
        const label = document.createElement('div');
        label.className = isRocket ? 'drone-label label-red' : 'drone-label';
        label.innerText = data.type;
        
        wrapper.appendChild(ico);
        wrapper.appendChild(label);

        const marker = new maplibregl.Marker({ element: wrapper }).setLngLat([data.lng, data.lat]).addTo(map);
        drones[id] = { marker, data };
        document.getElementById('count').innerText = Object.keys(drones).length;
    }

    // Слушаем базу данных в реальном времени
    onValue(targetsRef, (snapshot) => {
        const allTargets = snapshot.val();
        
        // Удаляем те, что пропали из базы
        for (let id in drones) {
            if (!allTargets || !allTargets[id]) {
                drones[id].marker.remove();
                delete drones[id];
            }
        }

        // Добавляем/обновляем цели
        if (allTargets) {
            for (let id in allTargets) {
                drawTarget(id, allTargets[id]);
            }
        }
        document.getElementById('count').innerText = Object.keys(drones).length;
    });

    // Анимация движения
    function animate() {
        for (let id in drones) {
            const d = drones[id];
            const speed = d.data.type.includes('РАКЕТА') ? 0.00006 : 0.000008;
            const rad = (d.data.angle - 90) * Math.PI / 180;
            d.data.lng += Math.cos(rad) * speed;
            d.data.lat -= Math.sin(rad) * speed;
            d.marker.setLngLat([d.data.lng, d.data.lat]);
        }
        requestAnimationFrame(animate);
    }
    animate();

    setInterval(() => {
        document.getElementById('clock').innerText = new Date().toLocaleTimeString('uk-UA');
    }, 1000);
</script>
</body>
</html>
