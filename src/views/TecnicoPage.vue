<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>📈 Técnico</ion-title>
      </ion-toolbar>
    </ion-header>


    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">🚀 Técnico</ion-title>
        </ion-toolbar>
      </ion-header>


      <!-- Grid principal del Dashboard -->
      <ion-grid class="dashboard-grid">
        <!-- 🟢 Fila 1: 3 Columnas -->
        <ion-row class="ion-row-1">
          <ion-col size="12" size-lg="4">
            <spark-line v-bind="sparkData1" />
          </ion-col>
          <ion-col size="6" size-lg="4">
            <spark-line v-bind="sparkData2" />
          </ion-col>
          <ion-col size="6" size-lg="4">
            <spark-line v-bind="sparkData3" />
          </ion-col>
        </ion-row>


        <!-- 🔵 Fila 2: 2 Columnas -->
        <ion-row class="ion-row-2">
          <ion-col size="12" size-md="3" push-md="9">
            <div class="box">
              <chart-js-doughnut
                :labels="donutData.labels"
                :values="donutData.values"
                :title="donutData.title"
                :description="donutData.description"
              />
            </div>
          </ion-col>
          <ion-col size="12" size-md="9" pull-md="3">
            <div class="box">
              <apex-mixed-chart :options="mixedChartData.options" :series="mixedChartData.series" />
            </div>
          </ion-col>
        </ion-row>


        <!-- 🟠 Fila 3: 3 Columnas -->
        <ion-row class="ion-row-3">
          <ion-col size="12" size-lg="4.5">
            <div class="box">
              <apex-line-r-t 
                :series="lineRTData.series"
                :title="lineRTData.title"
                :kpiTarget="lineRTData.kpiTarget"
                :color="lineRTData.color"
              />
            </div>
          </ion-col>
          <ion-col size="12" size-lg="4.5">
            <div class="box">
              <echarts-gauge 
                :value="bandwidthUsage"
                title="Uso de Ancho de Banda"
              />
            </div>
          </ion-col>
          <ion-col size="12" size-lg="3">
            <div class="box">
              <echarts-gauge-multiple :segments="ringSegments" />
            </div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>


<script setup lang="ts">
import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar, IonGrid, IonRow, IonCol } from '@ionic/vue';
import { ref, computed } from 'vue';
import SparkLine from '@/components/SparkLine.vue';
import ApexMixedChart from '@/components/ApexMixedChart.vue';
import ChartJsDoughnut from '@/components/ChartJsDoughnut.vue';
import ApexLineRT from '@/components/ApexLineRT.vue';
import EchartsGauge from '@/components/EchartsGauge.vue';
import EchartsGaugeMultiple from '@/components/EchartsGaugeMultiple.vue';

// Datos para el primer SparkLine (Tiempo de respuesta)
const sparkData1 = ref({
  title: "TIEMPO DE RESPUESTA",
  value: "180ms",
  bgColor: "gradient-blue",
  textColor: "white",
  iconName: "speedometer-outline",
  chartOptions: {
    chart: {
      id: 'response',
      type: 'line',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [250, 220, 200, 190, 185, 182, 180, 178, 179, 180] }],
});

// Datos para el segundo SparkLine (Uso de CPU)
const sparkData2 = ref({
  title: "USO DE CPU",
  value: "45%",
  bgColor: "gradient-green",
  textColor: "white",
  iconName: "hardware-chip-outline",
  chartOptions: {
    chart: {
      id: 'cpu',
      type: 'bar',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [65, 58, 52, 48, 45, 42, 45, 48, 46, 45] }],
});

// Datos para el tercer SparkLine (Memoria)
const sparkData3 = ref({
  title: "MEMORIA",
  value: "2.8GB",
  bgColor: "gradient-orange",
  textColor: "white",
  iconName: "server-outline",
  chartOptions: {
    chart: {
      id: 'memory',
      type: 'bar',
      sparkline: { enabled: true },
      dropShadow: { enabled: true, top: 1, left: 1, blur: 2, opacity: 0.5 }
    },
    stroke: { curve: 'smooth', width: 3 },
    colors: ['#fff'],
    tooltip: { theme: 'dark', x: { show: false }, y: { title: { formatter: () => '' } } }
  },
  chartSeries: [{ data: [3.2, 3.1, 3.0, 2.9, 2.8, 2.7, 2.8, 2.9, 2.8, 2.8] }],
});

// Datos para el gráfico de donut (Fila 2 - Columna Pequeña)
const donutData = computed(() => ({
  labels: ['Errores 500', 'Errores 400', 'Errores 300', 'Éxito'],
  values: [5, 15, 10, 70],
  title: 'Distribución de Errores',
  description: 'Porcentaje de errores por tipo'
}));

// Datos para el gráfico mixto (Fila 2 - Columna Grande)
const mixedChartData = ref({
  options: {
    chart: {
      type: 'line' as const,
      height: 350,
      toolbar: { show: false },
      background: '#1E1E1E'
    },
    stroke: {
      width: [0, 3],
      curve: 'smooth' as const
    },
    plotOptions: {
      bar: {
        columnWidth: '50%'
      }
    },
    colors: ['#00E396', '#FF4560', '#008FFB'],
    dataLabels: {
      enabled: false
    },
    labels: ['Ene', 'Feb', 'Mar', 'Abr', 'May', 'Jun', 'Jul', 'Ago', 'Sep', 'Oct'],
    xaxis: {
      type: 'category' as const,
      labels: { style: { colors: '#fff' } }
    },
    yaxis: [
      {
        title: { text: 'Errores', style: { color: '#fff' } },
        labels: { style: { colors: '#fff' } }
      },
      {
        opposite: true,
        title: { text: 'Tiempo (ms)', style: { color: '#fff' } },
        labels: { style: { colors: '#fff' } }
      }
    ],
    tooltip: {
      theme: 'dark'
    }
  },
  series: [
    {
      name: 'Errores de Red',
      type: 'column' as const,
      data: [45, 52, 38, 45, 19, 23, 20, 15, 12, 10]
    },
    {
      name: 'Errores de Servidor',
      type: 'column' as const,
      data: [35, 41, 36, 26, 45, 48, 52, 53, 41, 35]
    },
    {
      name: 'Tiempo de Respuesta',
      type: 'line' as const,
      data: [250, 220, 200, 190, 185, 182, 180, 178, 179, 180]
    }
  ]
});

// Datos para el gráfico de línea en tiempo real (Fila 3 - Columna 1)
const lineRTData = ref({
  series: [{
    name: 'Peticiones/seg',
    data: Array.from({ length: 20 }, (_, i) => ({
      x: new Date(Date.now() - (20 - i) * 1000).getTime(),
      y: Math.floor(Math.random() * 100) + 50
    }))
  }],
  title: 'Tráfico de Red',
  kpiTarget: 80,
  color: '#00E396'
});

// Datos para el gauge (Fila 3 - Columna 2)
const bandwidthUsage = ref(75); // Valor simulado del uso de ancho de banda

// Datos para el gauge múltiple (Fila 3 - Columna 3)
const ringSegments = ref([
  { value: 718, name: 'Descargas', color: '#f97316', min: 0, max: 1000 },
  { value: 224, name: 'Subidas', color: '#10b981', min: 0, max: 300 }
]);
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
  align-items: center;
  padding: 10px;
}


/* Aplicar altura total y por filas, solo en pantallas ≥ md */
@media (min-width: 992px) {  
  ion-grid{height: 100%;}
  .ion-row-1{height: 20%; max-height: 20%;}
  .ion-row-2{height: 40%; max-height: 40%;}
  .ion-row-3{height: 40%; max-height: 40%;}
}


</style>
