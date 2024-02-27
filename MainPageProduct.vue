<template>
  <ion-row>
    <ion-col>
      <div class="sa-welcome-screen-title">
        <h3>Рекомендуемые товары</h3>
        <ion-text color="primary" class="xs">Все</ion-text>
      </div>
    </ion-col>
  </ion-row>
  <ion-row>
    <ion-col>
      <div class="sa-products-horizontal-scroll">
        <Suspense>
          <template #default>
            <Products />
          </template>
          <template #fallback>
            <ProductsSkeleton />
          </template>
        </Suspense>
      </div>
    </ion-col>
  </ion-row>
</template>

<script setup lang="ts">
import Products from "./Products.vue";
import ProductsSkeleton from "./ProductsSkeleton.vue";
import ProductItem from "../../Product/ProductItem/ProductItem.vue";

import { IonRow, IonCol, IonText } from "@ionic/vue";
</script>
