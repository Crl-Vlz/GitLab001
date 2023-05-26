<template>
    <ion-page>
        <div v-if="signup" class="form">
            <ion-list>
                <ion-item>
                    <ion-input label="Correo Electronico" :value="email" @input="updateEmail($event.target.value)"
                        type="email" placeholder="direccion@mail.com"></ion-input>
                </ion-item>
                <ion-item>
                    <ion-input label="Contraseña" :value="pass" @input="updatePass($event.target.value)" type="password"
                        placeholder="*******"></ion-input>
                </ion-item>
                <ion-item>
                    {{}}
                </ion-item>
            </ion-list>
            <div class="btnGroup">
                <ion-button @click="changePage">Signup</ion-button>
                <ion-button @click="toggleSignup">Login</ion-button>
            </div>
        </div>
        <div v-else class="form">
            <ion-list>
                <ion-item>
                    <ion-input label="Correo Electronico" :value="email" @input="updateEmail($event.target.value)"
                        type="email" placeholder="direccion@mail.com"></ion-input>
                </ion-item>
                <ion-item>
                    <ion-input label="Contraseña" :value="pass" @input="updatePass($event.target.value)" type="password"
                        placeholder="*******"></ion-input>
                </ion-item>
                <ion-item>
                    {{}}
                </ion-item>
            </ion-list>
            <div class="btnGroup">
                <ion-button @click="changePage">Login</ion-button>
                <ion-button @click="toggleSignup">Signup</ion-button>
            </div>
        </div>
    </ion-page>
</template>

<script>
import { IonPage, IonButton, IonList, IonItem, IonInput } from '@ionic/vue';
import { useRouter } from 'vue-router';
import { ref as Iref } from 'vue';
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword } from 'firebase/auth'
import { getDatabase, set, ref } from 'firebase/database';

export default {
    setup() {
        const email = Iref('');
        const pass = Iref('');
        const err = Iref('');
        const signup = Iref(false);
        const router = useRouter();
        const auth = getAuth();
        const db = getDatabase();

        const updateEmail = (value) => {
            email.value = value;
        };

        const updatePass = (value) => {
            pass.value = value;
        };

        const changePage = async () => {
            if (signup.value === true) {
                //SIGNUP
                createUserWithEmailAndPassword(auth, email.value, pass.value)
                    .then((userCredential => {
                        const user = userCredential.user;
                        const uid = user.uid;
                        if (user == null) {
                            err.value = "No se pudo crear usuario"
                        } else {
                            set(ref(db, 'usuarios/' + uid), {
                                email: user.email
                            });
                            router.push('/tabs');
                        }
                    }))
                    .catch((error) => {
                        err.value = "Error durante creación del usuario"
                        console.log(error.message);
                    })
            } else if (signup.value === false) {
                //LOGIN
                signInWithEmailAndPassword(auth, email.value, pass.value)
                    .then((userCredential => {
                        const user = userCredential.user;
                        if (user == null) {
                            err.value = "No se pudo identificar usuario"
                        } else {
                            router.push('/tabs');
                        }
                    }))
                    .catch((error) => {
                        err.value = "Error al autentificar usuario"
                    })
            }
            console.log("Text: ", email.value, pass.value);
            //router.push('/tabs');
        };

        const toggleSignup = () => {
            signup.value = !signup.value;
            email.value = "";
            pass.value = "";
        };

        return { changePage, toggleSignup, email, pass, signup, updateEmail, updatePass };
    },
};
</script>

<style>
.form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    justify-self: center;
    align-self: self;
    align-items: center;
    width: 80vw;
    margin: auto;
    margin-top: 20vh;
}

.form ion-item {
    width: 80vw;
}

.btnGroup button {
    margin: auto;
    padding: 5vw;
}
</style>
