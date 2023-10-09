<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Settings</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Settings</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-grid>
        <ion-row>
          <ion-col v-for="i in 4">
            <ion-card>
              <ion-card-header>
                <ion-card-title>Setting {{ i }}</ion-card-title>
                <ion-card-subtitle>Card Subtitle</ion-card-subtitle>
              </ion-card-header>
          
              <ion-card-content>
                Here's a small text description for the card content. Nothing more, nothing less.
              </ion-card-content>
          
              <ion-button fill="clear">Action 1</ion-button>
              <ion-button fill="clear">Action 2</ion-button>
            </ion-card>
          </ion-col>
        </ion-row>
      </ion-grid>
      


    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import ExploreContainer from '@/components/ExploreContainer.vue';
</script>
