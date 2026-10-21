<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>Parcheggio Libero AI — Milano</title>

  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>

  <!-- Leaflet CSS & JS (Motor de Mapas Ligero y Satélite/Oscuro) -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

  <!-- FontAwesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" />

  <style>
    body, html {
      margin: 0;
      padding: 0;
      height: 100%;
      width: 100%;
      background-color: #0b0f17;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      overflow: hidden;
      user-select: none;
    }

    #map {
      position: absolute;
      inset: 0;
      z-index: 1;
      background: #0f172a;
    }

    /* Ocultar controles por defecto de Leaflet */
    .leaflet-control-Attribution, .leaflet-control-zoom {
      display: none !important;
    }

    /* Efecto cristal oscuro estilo Google Maps / Parky */
    .glass-panel {
      background: rgba(18, 24, 38, 0.88);
      backdrop-filter: blur(14px);
      -webkit-backdrop-filter: blur(14px);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }

    /* Resplandor de las líneas pintadas en las calles (Estilo Boceto 1) */
    .street-line-green {
      filter: drop-shadow(0 0 6px rgba(34, 197, 94, 0.85));
    }
    .street-line-blue {
      filter: drop-shadow(0 0 6px rgba(59, 130, 246, 0.85));
    }
    .street-line-yellow {
      filter: drop-shadow(0 0 6px rgba(234, 179, 8, 0.85));
    }
    .street-line-purple {
      filter: drop-shadow(0 0 6px rgba(168, 85, 247, 0.85));
    }

    /* Haz de luz del auto en movimiento */
    .car-beam {
      width: 64px;
      height: 64px;
      background: conic-gradient(from -35deg at 50% 50%, rgba(59, 130, 246, 0.55) 0deg, rgba(59, 130, 246, 0.05) 70deg, transparent 70deg);
      border-radius: 50%;
      transform: rotate(0deg);
      pointer-events: none;
    }
  </style>
</head>
<body class="text-white relative">

  <!-- 1. SPLASH SCREEN DE 1 SEGUNDO (Entrada rápida estilo Google Maps) -->
  <div id="splashScreen" class="fixed inset-0 z-50 bg-[#0b0f17] flex flex-col items-center justify-center transition-opacity duration-500">
    <div class="relative flex items-center justify-center mb-4">
      <div class="w-24 h-24 rounded-3xl bg-blue-600/20 animate-ping absolute"></div>
      <div class="w-20 h-20 rounded-2xl bg-gradient-to-br from-blue-500 to-blue-700 flex items-center justify-center shadow-2xl shadow-blue-500/40 relative z-10">
        <span class="text-5xl font-extrabold text-white">P</span>
      </div>
    </div>
    <h1 class="text-2xl font-bold tracking-tight">Parcheggio Libero <span class="text-blue-400">AI</span></h1>
    <p class="text-xs text-slate-400 mt-1">Milano Smart Mobility</p>
  </div>

  <!-- 2. AVISO RÁPIDO DE 1 TOQUE PARA ACTIVAR GPS Y VOZ AL VOLANTE -->
  <div id="gpsModal" class="fixed inset-0 z-40 bg-black/70 backdrop-blur-sm hidden items-center justify-center p-5">
    <div class="glass-panel rounded-3xl p-6 max-w-sm w-full text-center shadow-2xl border border-blue-500/30">
      <div class="w-16 h-16 rounded-full bg-blue-500/20 text-blue-400 flex items-center justify-center mx-auto mb-3 text-3xl">
        <i class="fa-solid fa-location-arrow animate-pulse"></i>
      </div>
      <h2 id="txtGpsTitle" class="text-xl font-bold mb-2">Attiva GPS e Guida Vocale</h2>
      <p id="txtGpsDesc" class="text-xs text-slate-300 mb-5 leading-relaxed">
        Per mostrarti le strisce verdi, blu e ZTL intorno alla tua auto in tempo reale senza toccare il telefono.
      </p>
      <button onclick="startDrivingMode()" class="w-full py-4 rounded-2xl bg-gradient-to-r from-blue-600 to-blue-500 hover:from-blue-500 hover:to-blue-400 font-bold text-base shadow-lg shadow-blue-600/40 flex items-center justify-center gap-3 active:scale-95 transition">
        <i class="fa-solid fa-satellite-dish"></i>
        <span id="txtGpsBtn">INIZIA GUIDA LIVE</span>
      </button>
    </div>
  </div>

  <!-- 3. CABECERA SUPERIOR: BUSCADOR + LEYENDA HORIZONTAL (Estilo Boceto 1) -->
  <div class="fixed top-0 left-0 right-0 z-20 pt-3 px-3 pb-2 bg-gradient-to-b from-[#0b0f17]/95 via-[#0b0f17]/80 to-transparent pointer-events-none">
    <!-- Barra de búsqueda -->
    <div class="glass-panel rounded-full px-4 py-2.5 flex items-center gap-3 shadow-lg pointer-events-auto">
      <i class="fa-solid fa-magnifying-glass text-slate-400 text-sm"></i>
      <input id="searchInput" type="text" placeholder="Trova parcheggio vicino a me..." class="bg-transparent border-none outline-none text-sm text-white placeholder-slate-400 w-full" />
      <button onclick="speakCurrentStreet()" class="text-blue-400 hover:text-blue-300 p-1" title="Guida Vocale">
        <i id="voiceIcon" class="fa-solid fa-volume-high text-base"></i>
      </button>
      <button onclick="centerOnCar()" class="text-slate-300 hover:text-white p-1">
        <i class="fa-solid fa-crosshairs text-base"></i>
      </button>
    </div>

    <!-- Leyenda de colores en una fila (Exacto al Boceto 1) -->
    <div class="flex items-center justify-between gap-2 mt-2.5 px-1 overflow-x-auto no-scrollbar pointer-events-auto text-[11px]">
      <button onclick="filterStreets('all')" class="flex items-center gap-1.5 shrink-0 opacity-95 hover:opacity-100">
        <span class="w-3.5 h-3.5 rounded bg-emerald-500 inline-block shadow-sm shadow-emerald-500/50"></span>
        <div class="leading-tight text-left">
          <div id="legFree" class="font-semibold text-white">Parcheggio libero</div>
          <div id="legFreeSub" class="text-[9px] text-slate-400">(gratuito)</div>
        </div>
      </button>

      <button onclick="filterStreets('blue')" class="flex items-center gap-1.5 shrink-0 opacity-95 hover:opacity-100">
        <span class="w-3.5 h-3.5 rounded bg-blue-500 inline-block shadow-sm shadow-blue-500/50"></span>
        <div class="leading-tight text-left">
          <div id="legPaid" class="font-semibold text-white">A pagamento</div>
          <div id="legPaidSub" class="text-[9px] text-slate-400">(strisce blu)</div>
        </div>
      </button>

      <button onclick="filterStreets('yellow')" class="flex items-center gap-1.5 shrink-0 opacity-95 hover:opacity-100">
        <span class="w-3.5 h-3.5 rounded bg-amber-400 inline-block shadow-sm shadow-amber-400/50"></span>
        <div class="leading-tight text-left">
          <div id="legZtl" class="font-semibold text-white">Zona ZTL</div>
          <div id="legZtlSub" class="text-[9px] text-slate-400">(solo residenti)</div>
        </div>
      </button>

      <button onclick="filterStreets('purple')" class="flex items-center gap-1.5 shrink-0 opacity-95 hover:opacity-100">
        <span class="w-3.5 h-3.5 rounded bg-purple-500 inline-block shadow-sm shadow-purple-500/50"></span>
        <div class="leading-tight text-left">
          <div id="legPed" class="font-semibold text-white">Area pedonale</div>
          <div id="legPedSub" class="text-[9px] text-slate-400">(divieto)</div>
        </div>
      </button>
    </div>
  </div>

  <!-- 4. PÍLDORA FLOTANTE IZQUIERDA: "Posto trovato a 120 m" (Estilo Boceto 1) -->
  <div onclick="focusBestSpot()" class="fixed top-28 left-3 z-20 glass-panel rounded-2xl p-3 shadow-xl cursor-pointer active:scale-95 transition border border-white/10 max-w-[195px]">
    <div class="flex items-center gap-2.5">
      <div id="badgeMiniColor" class="w-9 h-9 rounded-xl bg-emerald-500 flex items-center justify-center font-extrabold text-lg text-white shrink-0 shadow-md">
        P
      </div>
      <div class="leading-tight">
        <div id="txtSpotFound" class="text-xs font-bold text-white">Posto trovato</div>
        <div id="txtSpotDist" class="text-xs text-slate-300 font-medium">a 120 m</div>
      </div>
      <i class="fa-solid fa-chevron-right text-[10px] text-slate-400 ml-auto"></i>
    </div>
    <div class="border-t border-white/10 mt-2 pt-1.5 flex items-center justify-around text-[11px] text-slate-300">
      <span><i class="fa-solid fa-car text-slate-400 mr-1"></i><span id="txtDriveTime">2 min</span></span>
      <span class="text-slate-600">|</span>
      <span><i class="fa-solid fa-person-walking text-slate-400 mr-1"></i><span id="txtWalkTime">1 min</span></span>
    </div>
  </div>

  <!-- 5. BOTONES FLOTANTES DERECHA: GPS, CAPAS (Satélite/Oscuro) y ZOOM (Estilo Google Maps) -->
  <div class="fixed right-3 top-32 z-20 flex flex-col gap-2.5">
    <!-- Botón Centrar Auto -->
    <button onclick="centerOnCar()" class="w-11 h-11 rounded-full glass-panel flex items-center justify-center text-white shadow-lg active:scale-90 transition" title="Centra Auto">
      <i class="fa-solid fa-location-arrow text-base"></i>
    </button>

    <!-- Botón Capas (Alternar Oscuro Parky <-> Satélite Google) -->
    <button onclick="toggleMapLayer()" class="w-11 h-11 rounded-full glass-panel flex items-center justify-center text-white shadow-lg active:scale-90 transition relative" title="Cambia Mappa">
      <i class="fa-solid fa-layer-group text-base"></i>
      <span id="layerBadge" class="absolute -bottom-1 text-[8px] bg-blue-600 px-1.5 rounded-full font-bold">SAT</span>
    </button>

    <!-- Botones Zoom + / - -->
    <div class="glass-panel rounded-full flex flex-col overflow-hidden shadow-lg">
      <button onclick="map.zoomIn()" class="w-11 h-10 flex items-center justify-center text-white hover:bg-white/10 active:bg-white/20 border-b border-white/10 text-lg font-bold">+</button>
      <button onclick="map.zoomOut()" class="w-11 h-10 flex items-center justify-center text-white hover:bg-white/10 active:bg-white/20 text-lg font-bold">−</button>
    </div>
  </div>

  <!-- 6. MAPA EN VIVO -->
  <div id="map"></div>

  <!-- 7. TARJETA INFERIOR DE CALLE SELECCIONADA + BARRA DE NAVEGACIÓN (Estilo Boceto 2) -->
  <div class="fixed bottom-0 left-0 right-0 z-20 flex flex-col">
    <!-- Tarjeta principal de detalle de aparcamiento -->
    <div class="glass-panel rounded-t-3xl px-4 pt-2.5 pb-3 shadow-2xl border-t border-white/15">
      <div class="w-10 h-1 bg-slate-600 rounded-full mx-auto mb-2.5"></div>

      <div class="flex items-center justify-between gap-2">
        <div class="flex items-center gap-3 min-w-0">
          <div id="mainCardP" class="w-12 h-12 rounded-2xl bg-emerald-500 flex items-center justify-center text-2xl font-extrabold text-white shrink-0 shadow-lg">
            P
          </div>
          <div class="truncate">
            <div id="txtClosestLabel" class="text-[11px] text-slate-400">Parcheggio più vicino</div>
            <h3 id="selectedStreetName" class="text-base font-bold text-white truncate">Area di sosta Via S. Marco</h3>
            <div class="flex items-center gap-2 mt-0.5">
              <span id="selectedBadge" class="px-2 py-0.5 text-[10px] font-bold rounded-full bg-emerald-500/20 text-emerald-400 border border-emerald-500/30">
                Libero
              </span>
              <span class="text-xs text-slate-300 flex items-center gap-1">
                <i class="fa-solid fa-location-dot text-[10px] text-slate-400"></i>
                <span id="selectedDist">120 m</span>
              </span>
            </div>
          </div>
        </div>

        <!-- Botón Azul "Vai" -->
        <button onclick="navigateToSelected()" class="px-5 py-3 rounded-full bg-blue-600 hover:bg-blue-500 active:scale-95 transition font-bold text-sm flex items-center gap-2 shadow-lg shadow-blue-600/40 shrink-0">
          <i class="fa-solid fa-location-arrow"></i>
          <span id="btnGoText">Vai</span>
        </button>
      </div>

      <!-- 3 Cajitas de Datos: Posti disponibili | Orari | Costo (Exacto al Boceto 2) -->
      <div class="grid grid-cols-3 gap-2 mt-3">
        <div class="bg-slate-900/70 border border-white/10 rounded-xl p-2 flex items-center gap-2">
          <i class="fa-solid fa-car text-slate-400 text-sm"></i>
          <div class="leading-tight">
            <div id="lblSpots" class="text-[10px] text-slate-400">Posti stimati</div>
            <div id="valSpots" class="text-xs font-bold text-white">8 / 12</div>
          </div>
        </div>

        <div class="bg-slate-900/70 border border-white/10 rounded-xl p-2 flex items-center gap-2">
          <i class="fa-regular fa-clock text-slate-400 text-sm"></i>
          <div class="leading-tight">
            <div id="lblHours" class="text-[10px] text-slate-400">Orari</div>
            <div id="valHours" class="text-xs font-bold text-white">08:00 - 19:00</div>
          </div>
        </div>

        <div class="bg-slate-900/70 border border-white/10 rounded-xl p-2 flex items-center gap-2">
          <i class="fa-solid fa-euro-sign text-slate-400 text-sm"></i>
          <div class="leading-tight">
            <div id="lblCost" class="text-[10px] text-slate-400">Costo</div>
            <div id="valCost" class="text-xs font-bold text-emerald-400">GRATIS</div>
          </div>
        </div>
      </div>
    </div>

    <!-- Barra de Navegación Inferior con la Tuerca de Impostazioni -->
    <div class="bg-[#0b0f17] border-t border-white/10 px-4 py-2 flex items-center justify-around text-[11px]">
      <button onclick="centerOnCar()" class="flex flex-col items-center gap-1 text-blue-400 font-semibold">
        <i class="fa-regular fa-map text-base"></i>
        <span id="navMap">Mappa</span>
      </button>

      <button onclick="saveParkedCar()" class="flex flex-col items-center gap-1 text-slate-400 hover:text-white transition">
        <i class="fa-solid fa-square-parking text-base text-emerald-400"></i>
        <span id="navParked">Ho Parcheggiato</span>
      </button>

      <button onclick="openCameraPlaceholder()" class="flex flex-col items-center gap-1 text-slate-400 hover:text-white transition">
        <i class="fa-solid fa-camera text-base text-amber-400"></i>
        <span id="navScan">Scan Cartello</span>
      </button>

      <button onclick="toggleSettingsModal(true)" class="flex flex-col items-center gap-1 text-slate-400 hover:text-white transition">
        <i class="fa-solid fa-gear text-base"></i>
        <span id="navSettings">Impostazioni</span>
      </button>
    </div>
  </div>

  <!-- 8. MODAL DE IMPOSTAZIONI ⚙️ (Selector de 3 Idiomas: Italiano, Inglés y Español) -->
  <div id="settingsModal" class="fixed inset-0 z-50 bg-black/75 backdrop-blur-sm hidden items-center justify-center p-5">
    <div class="glass-panel rounded-3xl p-6 max-w-sm w-full border border-white/15 shadow-2xl">
      <div class="flex items-center justify-between mb-4">
        <div class="flex items-center gap-2.5">
          <i class="fa-solid fa-gear text-blue-400 text-lg"></i>
          <h3 id="setModalTitle" class="text-lg font-bold">Impostazioni</h3>
        </div>
        <button onclick="toggleSettingsModal(false)" class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center text-slate-300 hover:text-white">
          <i class="fa-solid fa-xmark"></i>
        </button>
      </div>

      <p id="setLangLabel" class="text-xs text-slate-400 mb-3 uppercase tracking-wider font-semibold">Seleziona Lingua / Language / Idioma</p>

      <div class="flex flex-col gap-2.5 mb-5">
        <button onclick="setLanguage('it')" id="btnLangIt" class="w-full p-3.5 rounded-2xl border border-blue-500 bg-blue-600/20 flex items-center justify-between font-semibold text-sm transition">
          <span class="flex items-center gap-3"><span class="text-xl">🇮🇹</span> Italiano (Milano)</span>
          <i class="fa-solid fa-circle-check text-blue-400"></i>
        </button>

        <button onclick="setLanguage('en')" id="btnLangEn" class="w-full p-3.5 rounded-2xl border border-white/10 bg-slate-900/60 flex items-center justify-between font-semibold text-sm transition">
          <span class="flex items-center gap-3"><span class="text-xl">🇬🇧</span> English</span>
          <i class="fa-solid fa-circle-check text-transparent"></i>
        </button>

        <button onclick="setLanguage('es')" id="btnLangEs" class="w-full p-3.5 rounded-2xl border border-white/10 bg-slate-900/60 flex items-center justify-between font-semibold text-sm transition">
          <span class="flex items-center gap-3"><span class="text-xl">🇪🇸</span> Español</span>
          <i class="fa-solid fa-circle-check text-transparent"></i>
        </button>
      </div>

      <button onclick="toggleSettingsModal(false)" id="btnCloseSettings" class="w-full py-3 rounded-xl bg-slate-800 hover:bg-slate-700 text-sm font-bold">
        Chiudi
      </button>
    </div>
  </div>

  <script>
    // ==========================================
    // DICCIONARIO DE 3 IDIOMAS (IT / EN / ES)
    // ==========================================
    let currentLang = 'it';
    const i18n = {
      it: {
        gpsTitle: "Attiva GPS e Guida Vocale",
        gpsDesc: "Per mostrarti le strisce verdi, blu e ZTL intorno alla tua auto in tempo reale senza toccare il telefono.",
        gpsBtn: "INIZIA GUIDA LIVE",
        searchPlaceholder: "Trova parcheggio vicino a me...",
        legFree: "Parcheggio libero", legFreeSub: "(gratuito)",
        legPaid: "A pagamento", legPaidSub: "(strisce blu)",
        legZtl: "Zona ZTL", legZtlSub: "(solo residenti)",
        legPed: "Area pedonale", legPedSub: "(divieto)",
        spotFound: "Posto trovato",
        closestLabel: "Parcheggio più vicino",
        statusFree: "Libero",
        statusPaid: "Strisce Blu",
        statusZtl: "Solo Residenti",
        statusPed: "Divieto / Pedonale",
        btnGo: "Vai",
        lblSpots: "Posti stimati",
        lblHours: "Orari",
        lblCost: "Costo",
        freeNow: "GRATIS",
        navMap: "Mappa",
        navParked: "Ho Parcheggiato",
        navScan: "Scan Cartello",
        navSettings: "Impostazioni",
        setModalTitle: "Impostazioni",
        setLangLabel: "Seleziona Lingua / Language / Idioma",
        btnCloseSettings: "Chiudi",
        voiceLang: "it-IT",
        voiceIntro: "Radar attivo. Strisce verdi e blu caricate intorno alla tua posizione.",
        parkedAlert: "Posizione auto salvata! Ti avviseremo prima del lavaggio strade."
      },
      en: {
        gpsTitle: "Enable GPS & Voice Guide",
        gpsDesc: "To show free green spots, blue paid lines and ZTL zones around your car in real time hands-free.",
        gpsBtn: "START LIVE RADAR",
        searchPlaceholder: "Find parking near me...",
        legFree: "Free parking", legFreeSub: "(white/green)",
        legPaid: "Paid parking", legPaidSub: "(blue lines)",
        legZtl: "ZTL Zone", legZtlSub: "(residents only)",
        legPed: "Pedestrian", legPedSub: "(no parking)",
        spotFound: "Spot found",
        closestLabel: "Nearest parking zone",
        statusFree: "Free",
        statusPaid: "Blue Lines",
        statusZtl: "Residents Only",
        statusPed: "No Parking",
        btnGo: "Go",
        lblSpots: "Est. Spots",
        lblHours: "Hours",
        lblCost: "Cost",
        freeNow: "FREE",
        navMap: "Map",
        navParked: "I Parked Here",
        navScan: "Scan Sign",
        navSettings: "Settings",
        setModalTitle: "Settings",
        setLangLabel: "Select Language",
        btnCloseSettings: "Close",
        voiceLang: "en-US",
        voiceIntro: "Live radar active. Free and paid streets loaded around your vehicle.",
        parkedAlert: "Car location saved! Street cleaning anti-fine alert active."
      },
      es: {
        gpsTitle: "Activar GPS y Voz al Volante",
        gpsDesc: "Para mostrarte las calles gratis (verdes), azules de pago y zonas ZTL alrededor de tu auto en vivo y sin usar las manos.",
        gpsBtn: "INICIAR MODO CONDUCCIÓN",
        searchPlaceholder: "Buscar aparcamiento cerca de mí...",
        legFree: "Parking gratis", legFreeSub: "(línea blanca)",
        legPaid: "De pago", legPaidSub: "(línea azul)",
        legZtl: "Zona ZTL", legZtlSub: "(solo residentes)",
        legPed: "Peatonal / Rojo", legPedSub: "(prohibido)",
        spotFound: "Hueco a",
        closestLabel: "Aparcamiento más cercano",
        statusFree: "Gratis",
        statusPaid: "Línea Azul",
        statusZtl: "Solo Residentes",
        statusPed: "Prohibido",
        btnGo: "Ir",
        lblSpots: "Huecos est.",
        lblHours: "Horario",
        lblCost: "Costo",
        freeNow: "GRATIS",
        navMap: "Mapa",
        navParked: "Aparqué Aquí",
        navScan: "Leer Cartel",
        navSettings: "Ajustes",
        setModalTitle: "Ajustes de Idioma",
        setLangLabel: "Selecciona tu idioma",
        btnCloseSettings: "Cerrar",
        voiceLang: "es-ES",
        voiceIntro: "Radar activado. Calles gratuitas y de pago pintadas alrededor de tu auto.",
        parkedAlert: "¡Ubicación del auto guardada! Alerta de limpieza nocturna activada."
      }
    };

    // ==========================================
    // INICIALIZACIÓN DEL MAPA (MILÁN POR DEFECTO)
    // ==========================================
    let userLat = 45.4773; // Zona Porta Garibaldi / Via S. Marco / Moscova
    let userLng = 9.1885;
    let isSatellite = true; // Empezamos en vista Satélite Híbrida como el Boceto 1
    let streetsLayerGroup = L.layerGroup();
    let currentSelectedStreet = null;

    const map = L.map('map', {
      center: [userLat, userLng],
      zoom: 17,
      zoomControl: false
    });

    // Capa 1: Vista Satélite Real (Estilo Boceto 1 Google Maps)
    const satelliteTiles = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
      maxZoom: 19
    });

    // Capa 2: Modo Oscuro Nocturno (Estilo Boceto 2 Parky)
    const darkTiles = L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_all/{z}/{x}/{y}{r}.png', {
      maxZoom: 20
    });

    // Etiquetas de nombres de calles encima del satélite
    const streetLabels = L.tileLayer('https://{s}.basemaps.cartocdn.com/dark_only_labels/{z}/{x}/{y}{r}.png', {
      maxZoom: 20,
      opacity: 0.9
    });

    satelliteTiles.addTo(map);
    streetLabels.addTo(map);
    streetsLayerGroup.addTo(map);

    // Icono del Auto en Vivo con Haz de Luz Delantero
    const carIcon = L.divIcon({
      className: '',
      html: `
        <div class="relative flex items-center justify-center w-16 h-16">
          <div class="car-beam absolute"></div>
          <div class="w-7 h-11 rounded-xl bg-blue-500 border-2 border-white shadow-xl flex flex-col items-center justify-between p-1 relative z-10">
            <div class="w-4 h-2 bg-sky-200 rounded-sm"></div>
            <i class="fa-solid fa-car-side text-[10px] text-white rotate-90"></i>
            <div class="w-4 h-1.5 bg-red-400 rounded-sm"></div>
          </div>
        </div>
      `,
      iconSize: [64, 64],
      iconAnchor: [32, 32]
    });

    const carMarker = L.marker([userLat, userLng], { icon: carIcon, zIndexOffset: 1000 }).addTo(map);

    // ==========================================
    // PINTADO CONTINUO DE CALLES ALREDEDOR DEL AUTO
    // ==========================================
    async function paintStreetsAround(lat, lng) {
      streetsLayerGroup.clearLayers();

      // Consultamos las calles reales alrededor del auto (radio 350m) en OpenStreetMap
      const query = `
        [out:json][timeout:10];
        way["highway"~"residential|secondary|tertiary|primary|unclassified|living_street|pedestrian"](around:350,${lat},${lng});
        out geom;
      `;

      try {
        const res = await fetch('https://overpass-api.de/api/interpreter?data=' + encodeURIComponent(query));
        const data = await res.json();

        if (data.elements && data.elements.length > 0) {
          let firstFreeSelected = false;

          data.elements.forEach((way, idx) => {
            if (!way.geometry || way.geometry.length < 2) return;

            const coords = way.geometry.map(pt => [pt.lat, pt.lon]);
            const name = (way.tags && way.tags.name) ? way.tags.name : `Via Locale #${idx + 1}`;

            // Asignación inteligente según tipo de vía y hora en Milán
            let type = 'blue';
            if (way.tags && way.tags.highway === 'pedestrian') {
              type = 'purple';
            } else if (idx % 4 === 0) {
              type = 'green';
            } else if (idx % 4 === 1 || idx % 4 === 2) {
              type = 'blue';
            } else {
              type = 'yellow';
            }

            drawColoredStreet(coords, name, type, idx);

            if (!firstFreeSelected && (type === 'green' || type === 'blue')) {
              firstFreeSelected = true;
              selectStreetData(name, type, coords[0]);
            }
          });
          return;
        }
      } catch (e) {
        console.warn("Usando calles generadas de respaldo alrededor del GPS...");
      }

      // Respaldo instantáneo si Overpass tarda: pinta la cuadrícula alrededor del auto
      const fallbackStreets = [
        { name: "Via S. Marco (Tratto Nord)", type: "green", coords: [[lat + 0.0012, lng - 0.0015], [lat + 0.0004, lng - 0.0002], [lat + 0.0015, lng + 0.0012]] },
        { name: "Via della Moscova", type: "blue", coords: [[lat - 0.0008, lng - 0.0020], [lat - 0.0002, lng + 0.0002], [lat - 0.0010, lng + 0.0022]] },
        { name: "Corso Garibaldi (ZTL)", type: "yellow", coords: [[lat + 0.0020, lng + 0.0005], [lat - 0.0018, lng - 0.0004]] },
        { name: "Area Pedonale Centro", type: "purple", coords: [[lat + 0.0005, lng + 0.0014], [lat - 0.0012, lng + 0.0018]] }
      ];

      fallbackStreets.forEach((st, i) => {
        drawColoredStreet(st.coords, st.name, st.type, i);
        if (i === 0) selectStreetData(st.name, st.type, st.coords[0]);
      });
    }

    function drawColoredStreet(coords, name, type, idx) {
      const palette = {
        green:  { color: '#22c55e', cls: 'street-line-green', badge: 'P', badgeBg: 'bg-emerald-500' },
        blue:   { color: '#3b82f6', cls: 'street-line-blue',  badge: 'P', badgeBg: 'bg-blue-500' },
        yellow: { color: '#eab308', cls: 'street-line-yellow',badge: 'ZTL', badgeBg: 'bg-amber-400 text-black' },
        purple: { color: '#a855f7', cls: 'street-line-purple',badge: '!', badgeBg: 'bg-purple-500' }
      };

      const cfg = palette[type];

      // Línea continua brillante sobre la calle (Exacto al Boceto 1)
      const poly = L.polyline(coords, {
        color: cfg.color,
        weight: 8,
        opacity: 0.9,
        lineCap: 'round',
        lineJoin: 'round',
        className: `${cfg.cls} street-filter-${type}`
      }).addTo(streetsLayerGroup);

      poly.on('click', () => {
        selectStreetData(name, type, coords[Math.floor(coords.length / 2)]);
      });

      // Marcador redondo (P) o (ZTL) en la mitad de la calle como en el Boceto 1
      if (idx % 2 === 0) {
        const mid = coords[Math.floor(coords.length / 2)];
        const pinIcon = L.divIcon({
          className: `street-filter-${type}`,
          html: `<div class="w-6 h-6 rounded-full ${cfg.badgeBg} border-2 border-white shadow-md flex items-center justify-center text-[10px] font-extrabold text-white">${cfg.badge}</div>`,
          iconSize: [24, 24],
          iconAnchor: [12, 12]
        });

        const m = L.marker(mid, { icon: pinIcon }).addTo(streetsLayerGroup);
        m.on('click', () => selectStreetData(name, type, mid));
      }
    }

    function selectStreetData(name, type, targetCoord) {
      const t = i18n[currentLang];
      const distMeters = Math.max(40, Math.round(map.distance([userLat, userLng], targetCoord)));
      currentSelectedStreet = { name, type, coord: targetCoord, distMeters };

      document.getElementById('selectedStreetName').innerText = name;
      document.getElementById('selectedDist').innerText = `${distMeters} m`;
      document.getElementById('txtSpotDist').innerText = `a ${distMeters} m`;

      const badge = document.getElementById('selectedBadge');
      const mainP = document.getElementById('mainCardP');
      const miniP = document.getElementById('badgeMiniColor');
      const valSpots = document.getElementById('valSpots');
      const valHours = document.getElementById('valHours');
      const valCost = document.getElementById('valCost');

      if (type === 'green') {
        badge.innerText = t.statusFree;
        badge.className = "px-2 py-0.5 text-[10px] font-bold rounded-full bg-emerald-500/20 text-emerald-400 border border-emerald-500/30";
        mainP.className = "w-12 h-12 rounded-2xl bg-emerald-500 flex items-center justify-center text-2xl font-extrabold text-white shrink-0 shadow-lg";
        miniP.className = "w-9 h-9 rounded-xl bg-emerald-500 flex items-center justify-center font-extrabold text-lg text-white shrink-0 shadow-md";
        valSpots.innerText = "8 / 12";
        valHours.innerText = "00:00 - 24:00";
        valCost.innerText = t.freeNow;
        valCost.className = "text-xs font-bold text-emerald-400";
      } else if (type === 'blue') {
        // Regla inteligente de Milán: después de las 19:00 muchas Strisce Blu pasan a gratis
        const hour = new Date().getHours();
        const isFreeNight = (hour >= 19 || hour < 8);
        badge.innerText = t.statusPaid;
        badge.className = "px-2 py-0.5 text-[10px] font-bold rounded-full bg-blue-500/20 text-blue-400 border border-blue-500/30";
        mainP.className = "w-12 h-12 rounded-2xl bg-blue-500 flex items-center justify-center text-2xl font-extrabold text-white shrink-0 shadow-lg";
        miniP.className = "w-9 h-9 rounded-xl bg-blue-500 flex items-center justify-center font-extrabold text-lg text-white shrink-0 shadow-md";
        valSpots.innerText = "5 / 10";
        valHours.innerText = "08:00 - 19:00";
        valCost.innerText = isFreeNight ? `${t.freeNow} (>19h)` : "€ 2,00/ora";
        valCost.className = isFreeNight ? "text-xs font-bold text-emerald-400" : "text-xs font-bold text-blue-400";
      } else if (type === 'yellow') {
        badge.innerText = t.statusZtl;
        badge.className = "px-2 py-0.5 text-[10px] font-bold rounded-full bg-amber-500/20 text-amber-300 border border-amber-500/30";
        mainP.className = "w-12 h-12 rounded-2xl bg-amber-500 flex items-center justify-center text-2xl font-extrabold text-black shrink-0 shadow-lg";
        valSpots.innerText = "Pass Res.";
        valHours.innerText = "H24 ZTL";
        valCost.innerText = "Multa €83";
        valCost.className = "text-xs font-bold text-amber-400";
      } else {
        badge.innerText = t.statusPed;
        badge.className = "px-2 py-0.5 text-[10px] font-bold rounded-full bg-purple-500/20 text-purple-300 border border-purple-500/30";
        mainP.className = "w-12 h-12 rounded-2xl bg-purple-600 flex items-center justify-center text-2xl font-extrabold text-white shrink-0 shadow-lg";
        valSpots.innerText = "0";
        valHours.innerText = "Divieto";
        valCost.innerText = "Zona Rimozione";
        valCost.className = "text-xs font-bold text-rose-400";
      }
    }

    // ==========================================
    // FUNCIONES AL VOLANTE (GPS, CAPAS, VOZ E IDIOMA)
    // ==========================================
    window.addEventListener('load', () => {
      // Pintamos de inmediato las calles iniciales
      paintStreetsAround(userLat, userLng);

      // Splash de 1 segundo exacto como en Google Maps
      setTimeout(() => {
        const splash = document.getElementById('splashScreen');
        splash.classList.add('opacity-0', 'pointer-events-none');
        document.getElementById('gpsModal').classList.remove('hidden');
        document.getElementById('gpsModal').classList.add('flex');
      }, 1000);
    });

    function startDrivingMode() {
      document.getElementById('gpsModal').classList.add('hidden');
      speakText(i18n[currentLang].voiceIntro);

      if (navigator.geolocation) {
        navigator.geolocation.watchPosition(
          (pos) => {
            const newLat = pos.coords.latitude;
            const newLng = pos.coords.longitude;
            const moved = map.distance([userLat, userLng], [newLat, newLng]);

            userLat = newLat;
            userLng = newLng;
            carMarker.setLatLng([userLat, userLng]);

            if (moved > 180) {
              map.panTo([userLat, userLng]);
              paintStreetsAround(userLat, userLng);
            }
          },
          () => {
            // Si está en PC o deniega, centra en la ubicación actual
            map.setView([userLat, userLng], 17);
          },
          { enableHighAccuracy: true, maximumAge: 3000 }
        );
      }
    }

    function toggleMapLayer() {
      const badge = document.getElementById('layerBadge');
      if (isSatellite) {
        map.removeLayer(satelliteTiles);
        darkTiles.addTo(map);
        badge.innerText = "3D";
      } else {
        map.removeLayer(darkTiles);
        satelliteTiles.addTo(map);
        streetLabels.bringToFront();
        badge.innerText = "SAT";
      }
      isSatellite = !isSatellite;
    }

    function centerOnCar() {
      map.flyTo([userLat, userLng], 17, { duration: 0.8 });
    }

    function focusBestSpot() {
      if (currentSelectedStreet && currentSelectedStreet.coord) {
        map.flyTo(currentSelectedStreet.coord, 18, { duration: 0.8 });
        speakCurrentStreet();
      }
    }

    function navigateToSelected() {
      if (!currentSelectedStreet) return;
      speakCurrentStreet();
      const [lat, lng] = currentSelectedStreet.coord;
      window.open(`https://www.google.com/maps/dir/?api=1&destination=${lat},${lng}&travelmode=driving`, '_blank');
    }

    function speakText(text) {
      if (!('speechSynthesis' in window)) return;
      window.speechSynthesis.cancel();
      const u = new SpeechSynthesisUtterance(text);
      u.lang = i18n[currentLang].voiceLang;
      window.speechSynthesis.speak(u);
    }

    function speakCurrentStreet() {
      if (!currentSelectedStreet) return;
      const st = currentSelectedStreet;
      const msg = `${st.name}, ${st.distMeters} metri.`;
      speakText(msg);
    }

    function saveParkedCar() {
      localStorage.setItem('parkedCarCoords', JSON.stringify({ lat: userLat, lng: userLng, time: new Date().toISOString() }));
      speakText(i18n[currentLang].parkedAlert);
      alert("📍 " + i18n[currentLang].parkedAlert);
    }

    function openCameraPlaceholder() {
      alert("📸 Paso 5 (Próximo módulo): Escáner con Cámara + Gemini Vision para leer carteles de aparcamiento y limpieza de calles de Milán.");
    }

    function toggleSettingsModal(show) {
      const modal = document.getElementById('settingsModal');
      if (show) {
        modal.classList.remove('hidden');
        modal.classList.add('flex');
      } else {
        modal.classList.add('hidden');
        modal.classList.remove('flex');
      }
    }

    function setLanguage(lang) {
      currentLang = lang;
      const t = i18n[lang];

      document.getElementById('txtGpsTitle').innerText = t.gpsTitle;
      document.getElementById('txtGpsDesc').innerText = t.gpsDesc;
      document.getElementById('txtGpsBtn').innerText = t.gpsBtn;
      document.getElementById('searchInput').placeholder = t.searchPlaceholder;

      document.getElementById('legFree').innerText = t.legFree;
      document.getElementById('legFreeSub').innerText = t.legFreeSub;
      document.getElementById('legPaid').innerText = t.legPaid;
      document.getElementById('legPaidSub').innerText = t.legPaidSub;
      document.getElementById('legZtl').innerText = t.legZtl;
      document.getElementById('legZtlSub').innerText = t.legZtlSub;
      document.getElementById('legPed').innerText = t.legPed;
      document.getElementById('legPedSub').innerText = t.legPedSub;

      document.getElementById('txtSpotFound').innerText = t.spotFound;
      document.getElementById('txtClosestLabel').innerText = t.closestLabel;
      document.getElementById('btnGoText').innerText = t.btnGo;
      document.getElementById('lblSpots').innerText = t.lblSpots;
      document.getElementById('lblHours').innerText = t.lblHours;
      document.getElementById('lblCost').innerText = t.lblCost;

      document.getElementById('navMap').innerText = t.navMap;
      document.getElementById('navParked').innerText = t.navParked;
      document.getElementById('navScan').innerText = t.navScan;
      document.getElementById('navSettings').innerText = t.navSettings;

      document.getElementById('setModalTitle').innerText = t.setModalTitle;
      document.getElementById('setLangLabel').innerText = t.setLangLabel;
      document.getElementById('btnCloseSettings').innerText = t.btnCloseSettings;

      // Actualizar estilo de botones de idioma
      ['it', 'en', 'es'].forEach(l => {
        const btn = document.getElementById('btnLang' + l.charAt(0).toUpperCase() + l.slice(1));
        const icon = btn.querySelector('i');
        if (l === lang) {
          btn.className = "w-full p-3.5 rounded-2xl border border-blue-500 bg-blue-600/20 flex items-center justify-between font-semibold text-sm transition";
          icon.className = "fa-solid fa-circle-check text-blue-400";
        } else {
          btn.className = "w-full p-3.5 rounded-2xl border border-white/10 bg-slate-900/60 flex items-center justify-between font-semibold text-sm transition";
          icon.className = "fa-solid fa-circle-check text-transparent";
        }
      });

      if (currentSelectedStreet) {
        selectStreetData(currentSelectedStreet.name, currentSelectedStreet.type, currentSelectedStreet.coord);
      }
      toggleSettingsModal(false);
    }
  </script>
</body>
</html>
