<template>
  <ion-card @click="goToProduct">
    <ion-row class="ion-flex ion-justify-content-center">
      <IonImg height="130" alt="product-img" :src="`assets/img/${img}`" />
    </ion-row>
    <ion-card-header>
      <ion-card-title>{{ price.toLocaleString("ru-RU") }} тг</ion-card-title>
      <ion-card-subtitle>{{ name }}</ion-card-subtitle>
    </ion-card-header>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonCard,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
  IonImg,
  IonRow,
  useIonRouter,
} from "@ionic/vue";

const props = defineProps({
  name: {
    type: String,
    default: "",
  },
  price: {
    type: Number,
    default: 0,
  },
  img: {
    type: String,
    default: "",
  },
  to: {
    type: String,
    default: "",
  },
});

const router = useIonRouter();

const goToProduct = () => {
  router.navigate(props.to, "forward", "push");
};
</script>

<style scoped>
ion-card-title {
  font-size: 12px;
  color: var(--ion-color-secondary-red-velvet);
}
ion-card-subtitle {
  font-size: 14px;
  color: var(--ion-color-primary-navy-black);
  overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 1;
}
ion-card {
  border-radius: 10px;
}
</style>
