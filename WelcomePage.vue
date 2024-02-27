<template>
  <ion-page>
    <main-page-header></main-page-header>
    <ion-content :fullscreen="true">
      <ion-grid class="main-screen">
        <main-page-search></main-page-search>
        <main-page-banner></main-page-banner>
        <main-page-categories></main-page-categories>
        <main-page-products></main-page-products>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import MainPageHeader from "../components/MainPage/Header/MainPageHeader.vue";
import MainPageProducts from "../components/MainPage/Product/MainPageProducts.vue";
import MainPageCategories from "../components/MainPage/Category/MainPageCategories.vue";
import MainPageBanner from "../components/MainPage/Banner/MainPageBanner.vue";
import MainPageSearch from "../components/MainPage/Search/MainPageSearch.vue";

import { IonPage, IonContent, IonGrid } from "@ionic/vue";
</script>
