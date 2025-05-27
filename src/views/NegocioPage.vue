<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>🚀 Negocio</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">🚀 Negocio</ion-title>
        </ion-toolbar>
      </ion-header>

      <!-- Grid principal del Dashboard -->
      <ion-grid class="dashboard-grid">
        <!-- 🟢 Fila 1: 4 Columnas -->
        <ion-row class="ion-row-1">
          <ion-col size="6" size-lg="3">
            <div class="box">
              <spark-line v-bind="sparkData1"/>
            </div>
          </ion-col>
          <ion-col size="6" size-lg="3">
            <div class="box">
              <spark-line v-bind="sparkData2"/>
            </div>
          </ion-col>
          <ion-col size="6" size-lg="3">
            <div class="box">
              <spark-line v-bind="sparkData3"/>
            </div>
          </ion-col>
          <ion-col size="6" size-lg="3">
            <div class="box">
              <spark-line v-bind="sparkData4"/>
            </div>
          </ion-col>
        </ion-row>

        <!-- 🟠 Fila 2: 2 Columnas -->
        <ion-row class="ion-row-3">
          <ion-col size="12" size-lg="8">
            <div class="box">
              <EchartsMap :data="dataDownloadsWorld" title="Distribución Global" subtitle="KPI: 20 Países > 5K" />
            </div>
          </ion-col>
          <ion-col size="12" size-lg="4">
            <div class="box">
              <ChartJsDoughnut 
                :labels="doughnutLabels" 
                :values="doughnutValues" 
                title="Top Países" 
                description="Distribución de descargas entre los 10 primeros países y el resto"
              />
            </div>
          </ion-col>
        </ion-row>

        <!-- 🔵 Fila 3: 2 Columnas -->
        <ion-row class="ion-row-2">
          <ion-col size="12" size-lg="8">
            <div class="box">
              <ApexMixedChart 
                :series="dataMixedChartSeries" 
              />
            </div>
          </ion-col>
          <ion-col size="12" size-lg="4">
            <div class="box">
              <EchartsGauge :value="dataGauge" title="SATISFACCIÓN" />
            </div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar, IonGrid, IonRow, IonCol } from '@ionic/vue';
import SparkLine from '@/components/SparkLine.vue';
import ApexMixedChart from '@/components/ApexMixedChart.vue';
import EchartsGauge from '@/components/EchartsGauge.vue';
import EchartsMap from '@/components/EchartsMap.vue';
import ChartJsDoughnut from '@/components/ChartJsDoughnut.vue';
import { ref, computed } from 'vue';

// Datos para el primer SparkLine (Visualizaciones)
const sparkData1 = ref({
  title: "VISUALIZACIONES",
  value: "2.5M",
  bgColor: "gradient-blue",
  textColor: "white",
  iconName: "eye-outline",
  chartOptions: {
    chart: {
      id: 'views',
      type: 'area',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [1500000, 1800000, 2100000, 1900000, 2300000, 2500000, 2200000, 2400000, 2600000, 2500000] }],
});

// Datos para el segundo SparkLine (Películas)
const sparkData2 = ref({
  title: "PELÍCULAS",
  value: "342K",
  bgColor: "gradient-green",
  textColor: "white",
  iconName: "film-outline",
  chartOptions: {
    chart: {
      id: 'movies',
      type: 'bar',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [20000, 40000, 50000, 80000, 120000, 180000, 220000, 290000, 320000, 342000] }],
});

// Datos para el tercer SparkLine (Series)
const sparkData3 = ref({
  title: "SERIES",
  value: "200K",
  bgColor: "gradient-orange",
  textColor: "white",
  iconName: "tv-outline",
  chartOptions: {
    chart: {
      id: 'series',
      type: 'bar',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [20000, 40000, 50000, 70000, 80000, 110000, 130000, 160000, 190000, 200000] }],
});

// Datos para el cuarto SparkLine (Usuarios)
const sparkData4 = ref({
  title: "USUARIOS",
  value: "45K",
  bgColor: "gradient-pink",
  textColor: "white",
  iconName: "people-outline",
  chartOptions: {
    chart: {
      id: 'users',
      type: 'line',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [25000, 30000, 35000, 32000, 38000, 42000, 40000, 45000, 48000, 45000] }],
});

// Datos para el gráfico mixto
const dataMixedChartSeries = ref([
  {
    name: 'Películas',
    type: 'area',
    data: [65, 58, 62, 70, 55, 60, 65, 70, 75],
    color: '#0396FF'  // Azul
  },
  {
    name: 'Series',
    type: 'area',
    data: [35, 42, 38, 30, 45, 40, 35, 30, 25],
    color: '#FF0000'  // Rojo
  },
  {
    name: 'Usuarios',
    type: 'column',
    data: [30, 25, 36, 30, 45, 35, 64, 52, 59],
    color: '#6be084'  // Verde
  }
]);

// Datos para el mapa
const dataDownloadsWorld = ref([
  { name: "United States of America", value: 18000 },
  { name: "China", value: 17000 },
  { name: "India", value: 16000 },
  { name: "Brazil", value: 14000 },
  { name: "Russia", value: 13000 },
  { name: "Germany", value: 15000 },
  { name: "France", value: 12000 },
  { name: "United Kingdom", value: 11000 },
  { name: "Japan", value: 12500 },
  { name: "Canada", value: 9500 },
  { name: "Italy", value: 9000 },
  { name: "South Korea", value: 8700 },
  { name: "Mexico", value: 7800 },
  { name: "Indonesia", value: 7200 },
  { name: "Spain", value: 7000 },
  { name: "Australia", value: 6800 },
  { name: "Turkey", value: 6400 },
  { name: "Saudi Arabia", value: 6000 },
  { name: "Argentina", value: 5400 }
]);

// Computados para top 10 + "Otros"
const sorted = computed(() =>
  [...dataDownloadsWorld.value].sort((a, b) => b.value - a.value)
);
const top10 = computed(() => sorted.value.slice(0, 10));
const others = computed(() =>
  sorted.value.slice(10).reduce((sum, c) => sum + c.value, 0)
);

const doughnutLabels = computed(() => [
  'Estados Unidos',
  'China',
  'India',
  'Alemania',
  'Brasil',
  'Rusia',
  'Francia',
  'Reino Unido',
  'Japón',
  'Canadá',
  'Otros'
]);

const doughnutValues = computed(() => [
  18000,
  17000,
  16000,
  15000,
  14000,
  13000,
  12000,
  11000,
  12500,
  9500,
  others.value
]);

// Datos para el medidor
const dataGauge = ref(85);

</script>

<style scoped>
ion-row{
  overflow: hidden;
}

ion-col {
  max-height: 100%;
  --ion-grid-column-padding:10px;
}

/* El contenido real de cada columna */
.box {
  background: #1E1E1E;
  height: 100%;
  max-height: 100%;
  overflow: hidden;
  border-radius:5px;
  display: flex;
  justify-content: center;
  align-items: start;
}

/* Aplicar altura total y por filas, solo en pantallas ≥ md */
@media (min-width: 992px) {  
  ion-grid{height: 100%;}
  .ion-row-1{height: 20%; max-height: 20%;}
  .ion-row-2{height: 40%; max-height: 40%;}
  .ion-row-3{height: 40%; max-height: 40%;}
}
</style>
