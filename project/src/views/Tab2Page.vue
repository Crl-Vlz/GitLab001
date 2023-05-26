<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Usuarios</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Usuarios</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-grid>
        <ion-row>
          <ion-col>
            <div>Correo</div>
          </ion-col>
        </ion-row>
        <ion-row v-for=" user in users">
          <ion-col>
            <div>{{ user.email }}</div>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script>

import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonCol,
  IonGrid,
  IonRow,
} from "@ionic/vue";
import { getDatabase, ref, onValue } from "firebase/database";
export default {
  name: "Tab1",
  components: {
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonPage,
    IonCol,
    IonGrid,
    IonRow,
  },
  mounted() {

    const db = getDatabase();
    const usersRef = ref(db, 'usuarios');

    onValue(usersRef, (snapshot) => {
      this.users = snapshot.val();
    });
  },
  data() {
    return {
      users: [],
    }
  }
};
</script>

<style scoped>
ion-col>div {
  background-color: #00933b;
  padding: 10px;
  display: flex;
  justify-content: center;
  border-style: solid;
  border-width: 0.1em;
  border-color: #fdd923;
  ;
}
</style>
