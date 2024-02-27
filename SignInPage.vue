<template>
  <ion-page>
    <ion-content>
      <ion-grid :fixed="true">
        <ion-row>
          <ion-col>
            <ion-text>
              <h1>
                Добро<br />
                пожаловать!
              </h1>
            </ion-text>
          </ion-col>
        </ion-row>
        <ion-row>
          <ion-col>
            <ion-text>
              <p class="subtitle-dark-grey">Войдите чтобы совершать покупки</p>
            </ion-text>
          </ion-col>
        </ion-row>
        <Form
          @submit="onSubmit"
          :validation-schema="schema"
          v-slot="{ errors, isSubmitting }"
          :validate-on-mount="true"
        >
          <ion-row>
            <ion-col>
              <ion-label class="sa-label">Email</ion-label>
              <Field name="email" v-slot="{ field }">
                <ion-input
                  placeholder="mail@email.com"
                  class="sa-input"
                  v-bind="field"
                  v-model="email"
                ></ion-input>
              </Field>
            </ion-col>
          </ion-row>
          <ion-row>
            <ion-col>
              <ion-label class="sa-label">Пароль</ion-label>
              <Field name="password" v-slot="{ field }">
                <ion-input
                  type="password"
                  placeholder="Введите пароль"
                  class="sa-input"
                  v-bind="field"
                  v-model="password"
                ></ion-input>
              </Field>
            </ion-col>
          </ion-row>
          <ion-row>
            <ion-col>
              <ion-button
                expand="block"
                type="submit"
                :disabled="isSubmitting || Object.keys(errors).length > 0"
                class="btn-primary-red"
              >
                <span v-show="!isSubmitting">Войти</span>
                <ion-spinner
                  v-show="isSubmitting"
                  name="crescent"
                ></ion-spinner>
              </ion-button>
            </ion-col>
          </ion-row>
        </Form>
        <ion-row class="ion-justify-content-between">
          <ion-col><ion-text>Забыли пароль</ion-text></ion-col>
          <ion-col class="text-end"
            ><ion-text :color="'primary'" router-link="/sign-up"
              >Регистрация</ion-text
            ></ion-col
          >
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonContent,
  IonGrid,
  IonCol,
  IonRow,
  IonText,
  IonInput,
  IonLabel,
  IonButton,
  IonSpinner,
} from "@ionic/vue";
import { ref } from "vue";
import { Form, Field } from "vee-validate";
import * as Yup from "yup";

import { useAuthStore } from "@/stores/auth.store";

const email = ref("");
const password = ref("");

const schema = Yup.object().shape({
  email: Yup.string()
    .email("Неправильный формат email")
    .required("Поле email обязательно"),
  password: Yup.string().required("Поле пароль обязательно"),
});

async function onSubmit(values: any, { setErrors }: any) {
  const authStore = useAuthStore();
  const { email, password } = values;

  try {
    return await authStore.login(email, password);
  } catch (error) {
    return setErrors({ apiError: error });
  }
}
</script>

<style scoped>
ion-grid {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: end;
}
form {
  margin-top: 50px;
  margin-bottom: 100px;
}
form ion-row {
  margin-top: 30px;
}
form ion-row:first-child {
  margin-top: 0px;
}
form ion-row:last-child {
  margin-top: 70px;
}
ion-row:last-child {
  padding-bottom: 30px;
}
ion-spinner {
  height: 14px;
}
</style>
