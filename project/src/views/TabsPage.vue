<template>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="tab1" href="/tabs/tab1">
          <ion-icon aria-hidden="true" :icon="serverOutline" />
          <ion-label>Monitoreo de claves</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="tab2" href="/tabs/tab2">
          <ion-icon aria-hidden="true" :icon="personCircleOutline" />
          <ion-label>Monitoreo de usuarios</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="tab3" href="/tabs/tab3">
          <ion-icon aria-hidden="true" :icon="keyOutline" />
          <ion-label>Generación de contraseñas</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script setup>
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage, IonRouterOutlet } from '@ionic/vue';
import { ellipse, square, triangle, personCircleOutline, serverOutline, keyOutline } from 'ionicons/icons';
</script>

<style scoped>
  ion-tab-bar {
    background-color: #00933b;
  }
  ion-tab-button {
    background-color: #00933b;
    color: white;
  }
  .tab-selected {
    color: #fdd923;
  }
</style>