<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>My Habits</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">My Habits</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-list v-for="i in 5">
        <ion-list-header>
          <ion-skeleton-text
            :animated="true"
            style="width: 80px"
          ></ion-skeleton-text>
        </ion-list-header>
        <ion-item>
          <ion-thumbnail slot="start">
            <ion-skeleton-text :animated="true"></ion-skeleton-text>
          </ion-thumbnail>
          <ion-label>
            <h3>
              <ion-skeleton-text
                :animated="true"
                style="width: 80%"
              ></ion-skeleton-text>
            </h3>
            <p>
              <ion-skeleton-text
                :animated="true"
                style="width: 60%"
              ></ion-skeleton-text>
            </p>
            <p>
              <ion-skeleton-text
                :animated="true"
                style="width: 30%"
              ></ion-skeleton-text>
            </p>
          </ion-label>
        </ion-item>
      </ion-list>

    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";
import ExploreContainer from "@/components/ExploreContainer.vue";
</script>
