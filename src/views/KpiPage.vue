<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>🎯 KPIs</ion-title>
      </ion-toolbar>
    </ion-header>


    <ion-content :fullscreen="true" class="ion-padding">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">🎯 KPIs</ion-title>
        </ion-toolbar>
      </ion-header>


      <h1 class="ion-padding">🚀 KPIs de Negocio</h1>
      <ion-accordion-group expand="inset" :multiple="true">
        <ion-accordion v-for="item in smartGoals" :key="item.id" :value="item.id.toString()">
          <ion-item slot="header">
            <ion-label>{{ item.id }}. {{ item.title }}</ion-label>
          </ion-item>
          <div class="ion-padding" slot="content">
            <p>{{ item.description }}</p>
            <ion-list :inset="true">
              <ion-item v-for="(element, index) in item.smart" :key="index">
                <ion-label><b>{{ element.letter }}</b> → {{ element.content }}</ion-label>
              </ion-item>
            </ion-list>
          </div>
        </ion-accordion>
      </ion-accordion-group>
      <br>
      <h1 class="ion-padding">📈 KPIs Técnicos</h1>
      <ion-accordion-group expand="inset" :multiple="true">
        <ion-accordion v-for="item in technicalGoals" :key="item.id" :value="item.id.toString()">
          <ion-item slot="header">
            <ion-label>{{ item.id }}. {{ item.title }}</ion-label>
          </ion-item>
          <div class="ion-padding" slot="content">
            <p>{{ item.description }}</p>
            <ion-list :inset="true">
              <ion-item v-for="(element, index) in item.smart" :key="index">
                <ion-label><b>{{ element.letter }}</b> → {{ element.content }}</ion-label>
              </ion-item>
            </ion-list>
          </div>
        </ion-accordion>
      </ion-accordion-group>
    </ion-content>
  </ion-page>
</template>


<script setup lang="ts">
import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar, IonAccordionGroup, IonAccordion, IonItem, IonLabel, IonList } from '@ionic/vue';
import { ref } from 'vue';


// Definición de la estructura de datos para un objetivo SMART
interface SmartElement {
  letter: string;
  content: string;
}


interface SmartGoal {
  id: number;
  title: string;
  description: string;
  smart: SmartElement[];
}


// Array de objetivos SMART de negocio
const smartGoals = ref<SmartGoal[]>([
  {
    id: 1,
    title: "Aumentar visualizaciones",
    description: "Aumentar las visualizaciones totales en un 50% (de 2.5M a 3.75M) en los siguientes 3 meses, mediante la optimización del catálogo y la mejora de la experiencia de usuario.",
    smart: [
      { letter: "S", content: "Aumentar las visualizaciones totales en un 50%" },
      { letter: "M", content: "50% (de 2.5M a 3.75M visualizaciones)" },
      { letter: "A", content: "mediante la optimización del catálogo y la mejora de la experiencia de usuario" },
      { letter: "R", content: "para aumentar el engagement y la retención de usuarios" },
      { letter: "T", content: "en los siguientes 3 meses" }
    ]
  },
  {
    id: 2,
    title: "Crecimiento de usuarios",
    description: "Aumentar la base de usuarios activos en un 30% (de 45K a 58.5K) en los próximos 6 meses, implementando un programa de referidos y mejorando la visibilidad en redes sociales.",
    smart: [
      { letter: "S", content: "Aumentar la base de usuarios activos en un 30%" },
      { letter: "M", content: "30% (de 45K a 58.5K usuarios)" },
      { letter: "A", content: "implementando un programa de referidos y mejorando la visibilidad en redes sociales" },
      { letter: "R", content: "para expandir nuestra base de usuarios y aumentar el alcance" },
      { letter: "T", content: "en los próximos 6 meses" }
    ]
  },
  {
    id: 3,
    title: "Balance de contenido",
    description: "Alcanzar un balance 60/40 entre películas y series (actualmente 65/35) para finales del año, mediante la adquisición estratégica de contenido y el desarrollo de series originales.",
    smart: [
      { letter: "S", content: "Alcanzar un balance 60/40 entre películas y series" },
      { letter: "M", content: "60% películas, 40% series (actualmente 65/35)" },
      { letter: "A", content: "mediante la adquisición estratégica de contenido y el desarrollo de series originales" },
      { letter: "R", content: "para diversificar la oferta y aumentar el tiempo de visualización" },
      { letter: "T", content: "para finales del año" }
    ]
  },
  {
    id: 4,
    title: "Expansión internacional",
    description: "Aumentar la presencia en mercados internacionales, logrando que 5 nuevos países alcancen más de 10K visualizaciones mensuales en los próximos 12 meses.",
    smart: [
      { letter: "S", content: "Aumentar la presencia en mercados internacionales" },
      { letter: "M", content: "5 nuevos países con más de 10K visualizaciones mensuales" },
      { letter: "A", content: "mediante la localización de contenido y campañas específicas por país" },
      { letter: "R", content: "para expandir el alcance global y diversificar la base de usuarios" },
      { letter: "T", content: "en los próximos 12 meses" }
    ]
  },
  {
    id: 5,
    title: "Satisfacción de usuarios",
    description: "Mejorar la satisfacción de usuarios del 85% al 95% en un período de 6 meses, implementando mejoras en la interfaz y optimizando la calidad del streaming.",
    smart: [
      { letter: "S", content: "Mejorar la satisfacción de usuarios" },
      { letter: "M", content: "del 85% al 95% de satisfacción" },
      { letter: "A", content: "implementando mejoras en la interfaz y optimizando la calidad del streaming" },
      { letter: "R", content: "para aumentar la retención y reducir la tasa de abandono" },
      { letter: "T", content: "en un período de 6 meses" }
    ]
  }
]);

// Array de objetivos SMART técnicos
const technicalGoals = ref<SmartGoal[]>([
  {
    id: 1,
    title: "Tiempo de carga",
    description: "Reducir el tiempo de carga inicial de la aplicación de 3.5s a menos de 2s en los próximos 3 meses, mediante la optimización de assets y la implementación de lazy loading.",
    smart: [
      { letter: "S", content: "Reducir el tiempo de carga inicial de la aplicación" },
      { letter: "M", content: "de 3.5s a menos de 2s" },
      { letter: "A", content: "mediante la optimización de assets y la implementación de lazy loading" },
      { letter: "R", content: "para mejorar la experiencia de usuario y reducir la tasa de rebote" },
      { letter: "T", content: "en los próximos 3 meses" }
    ]
  },
  {
    id: 2,
    title: "Tasa de errores",
    description: "Reducir la tasa de errores de la aplicación del 2% al 0.5% en los próximos 6 meses, implementando un sistema robusto de monitoreo y manejo de errores.",
    smart: [
      { letter: "S", content: "Reducir la tasa de errores de la aplicación" },
      { letter: "M", content: "del 2% al 0.5%" },
      { letter: "A", content: "implementando un sistema robusto de monitoreo y manejo de errores" },
      { letter: "R", content: "para aumentar la confiabilidad y estabilidad de la plataforma" },
      { letter: "T", content: "en los próximos 6 meses" }
    ]
  },
  {
    id: 3,
    title: "Rendimiento de streaming",
    description: "Mejorar la calidad del streaming para que el 99% de las reproducciones se inicien en menos de 2 segundos, optimizando la infraestructura de CDN y el sistema de caché.",
    smart: [
      { letter: "S", content: "Mejorar la calidad del streaming" },
      { letter: "M", content: "99% de reproducciones en menos de 2 segundos" },
      { letter: "A", content: "optimizando la infraestructura de CDN y el sistema de caché" },
      { letter: "R", content: "para proporcionar una experiencia de visualización fluida" },
      { letter: "T", content: "en los próximos 4 meses" }
    ]
  },
  {
    id: 4,
    title: "Cobertura de pruebas",
    description: "Aumentar la cobertura de pruebas automatizadas del 65% al 90% del código base en los próximos 8 meses, implementando pruebas unitarias, de integración y end-to-end.",
    smart: [
      { letter: "S", content: "Aumentar la cobertura de pruebas automatizadas" },
      { letter: "M", content: "del 65% al 90% del código base" },
      { letter: "A", content: "implementando pruebas unitarias, de integración y end-to-end" },
      { letter: "R", content: "para garantizar la calidad y estabilidad del código" },
      { letter: "T", content: "en los próximos 8 meses" }
    ]
  },
  {
    id: 5,
    title: "Optimización de recursos",
    description: "Reducir el consumo de recursos del servidor en un 40% en los próximos 6 meses, mediante la implementación de técnicas de optimización y el uso de tecnologías más eficientes.",
    smart: [
      { letter: "S", content: "Reducir el consumo de recursos del servidor" },
      { letter: "M", content: "reducción del 40% en consumo de recursos" },
      { letter: "A", content: "mediante la implementación de técnicas de optimización y el uso de tecnologías más eficientes" },
      { letter: "R", content: "para mejorar la escalabilidad y reducir costos operativos" },
      { letter: "T", content: "en los próximos 6 meses" }
    ]
  }
]);


</script>


<style scoped>


ion-accordion.accordion-collapsing ion-item[slot='header'],
  ion-accordion.accordion-collapsed ion-item[slot='header'] {
    --background: var(--ion-color-light);
    --color: var(--ion-color-light-contrast);
  }


  ion-accordion.accordion-expanding ion-item[slot='header'],
  ion-accordion.accordion-expanded ion-item[slot='header'] {
    --background: rgba(var(--ion-color-primary-rgb), 0.14);
    color: var(--ion-color-primary);
  }


</style>
