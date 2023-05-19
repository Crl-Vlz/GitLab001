<template>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
</template>

<script setup>
import { IonApp, IonRouterOutlet } from '@ionic/vue';
import {getAuth, signInWithEmailAndPassword} from "firebase/auth";

const auth = getAuth();
signInWithEmailAndPassword(auth, "test@mail.com", "password01")
  .then((userCrendential) => {
    const user = userCrendential.user;
    if (user == null){
      console.log("Not authentificated")
    } else {
      console.log("User verified")
    }
  })
  .catch((error) => {
    const errorCode = error.code
    const errorMessage = error.message
    console.log(errorCode, errorMessage)
  });

</script>
