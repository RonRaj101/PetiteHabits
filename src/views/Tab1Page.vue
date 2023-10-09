<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Home</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Home</ion-title>
        </ion-toolbar>
      </ion-header>

    
      <ion-list expand="block" class="ion-padding">
        <ion-list-header>
          <h1>Popular Habits</h1>
        </ion-list-header>

        <ion-row class="ion-justify-content-start">
          <ion-col size="">
            
            <ion-item color="primary" @click="setOpenPreset(true, 'read')" button>
              <ion-label slot="start">Reading</ion-label>
              <ion-icon :icon="book" slot="end"></ion-icon>
          </ion-item>
          
        </ion-col>

        <ion-col size="">
          
          <ion-item color="secondary" @click="setOpenPreset(true, 'exercise')" button>
            <ion-label slot="start">Exercise</ion-label>
            <ion-icon :icon="body" slot="end"></ion-icon>
        </ion-item>
          
        </ion-col>

        <ion-col size="">
          
            <ion-item color="tertiary" @click="setOpenPreset(true, 'meditate')" button>
                <ion-label slot="start">Meditation</ion-label>
                <ion-icon :icon="batteryCharging" slot="end"></ion-icon>
            </ion-item>
          
        </ion-col>

        <ion-col size="">
          
            <ion-item color="success" @click="setOpenPreset(true, 'socialise')" >
              
              
                <ion-label>Socialise</ion-label>
                <ion-icon :icon="people" slot="end"></ion-icon>
              
            </ion-item>
          
        </ion-col>

        </ion-row>
      </ion-list>

      <!-- Custom Habits Modal Button -->
      <ion-grid class="ion-padding">
        <ion-list-header>
          <h1>Create Custom</h1>
        </ion-list-header>
        <ion-row>
          <ion-col>
            <ion-button @click="setOpen(true)" expand="block" color="medium"
              >Create Custom Habit
              <ion-icon slot="end" :icon="addCircleOutline"></ion-icon
            ></ion-button>
          </ion-col>
        </ion-row>
      </ion-grid>

      <!-- Custom Habits Modal -->
      <ion-modal :is-open="isOpen">
        <ion-header>
          <ion-toolbar>
            <ion-buttons slot="start">
              <ion-button @click="setOpen(false)">Cancel</ion-button>
            </ion-buttons>
            <ion-title></ion-title>
            <ion-buttons slot="end">
              <ion-button :strong="true">Confirm</ion-button>
            </ion-buttons>
          </ion-toolbar>
        </ion-header>

        <ion-content class="ion-padding">
          <ion-list>
            <ion-item>
              <ion-input labelPlacement="floating" value="">
                <div slot="label">Title</div>
              </ion-input>
            </ion-item>
  
            <ion-item>
              <ion-textarea labelPlacement="floating" value="">
                <div slot="label">
                  Description <ion-text color="medium">(Optional)</ion-text>
                </div>
              </ion-textarea>
            </ion-item>
  
            <ion-item>
              <ion-label>Choose starting date/time</ion-label>
              <ion-datetime-button datetime="datetime"></ion-datetime-button>
              <ion-modal :keep-contents-mounted="true">
                <ion-datetime id="datetime"></ion-datetime>
              </ion-modal>
            </ion-item>
  
            <ion-item>
              <ion-select
                label="Reminder Frequency"
                label-placement="floating"
                v-model="frequency"
              >
                <ion-select-option value="Daily">Daily</ion-select-option>
                <ion-select-option value="Weekly">Weekly</ion-select-option>
                <ion-select-option value="Monthly">Monthly</ion-select-option>
                <ion-select-option value="Custom"
                  >Custom Frequency</ion-select-option
                >
              </ion-select>
            </ion-item>
            <ion-item v-if="frequency === 'Custom'">
              <ion-list>
                <ion-item>
                  <ion-select
                    label="Repeat Frequency"
                    label-placement="floating"
                    v-model="repeatingFrequency"
                  >
                    <ion-select-option value="Day"
                      >Repeat Daily</ion-select-option
                    >
                    <ion-select-option value="Week"
                      >Repeat Weekly</ion-select-option
                    >
                    <ion-select-option value="Month"
                      >Repeat Monthly</ion-select-option
                    >
                    <ion-select-option value="Year"
                      >Repeat Annually</ion-select-option
                    >
                  </ion-select>
  
                  <ion-list
                    v-if="repeatingFrequency == 'Week'"
                    id="weeklyRepeatDays"
                  >
                    <ion-item>
                      <ion-checkbox name="Monday" justify="start"
                        >Monday</ion-checkbox
                      >
                    </ion-item>
                    <ion-item>
                      <ion-checkbox name="Tuesday" justify="start"
                        >Tuesday</ion-checkbox
                      >
                    </ion-item>
                    <ion-item>
                      <ion-checkbox name="Wednesday" justify="start"
                        >Wednesday</ion-checkbox
                      >
                    </ion-item>
                    <ion-item>
                      <ion-checkbox name="Thursday" justify="start"
                        >Thursday</ion-checkbox
                      >
                    </ion-item>
                    <ion-item>
                      <ion-checkbox name="Friday" justify="start"
                        >Friday</ion-checkbox
                      >
                    </ion-item>
                    <ion-item>
                      <ion-checkbox name="Saturday" justify="start"
                        >Saturday</ion-checkbox
                      >
                    </ion-item>
                    <ion-item>
                      <ion-checkbox name="Sunday" justify="start"
                        >Sunday</ion-checkbox
                      >
                    </ion-item>
                  </ion-list>
                </ion-item>
  
                <ion-item>
                  <ion-input
                    type="number"
                    labelPlacement="floating"
                    value="1"
                    v-model="repeatEveryVal"
                  >
                    <div slot="label">
                      Repeat Every {{ repeatEveryVal }}
                      <ion-text color="">{{ repeatingFrequency }}s</ion-text>
                    </div>
                  </ion-input>
                </ion-item>
  
                <ion-item>
                  <ion-select
                    label="Repeat Till"
                    label-placement="floating"
                    v-model="repeatingTill"
                  >
                    <ion-select-option value="forever"
                      >Indefinetely</ion-select-option
                    >
                    <ion-select-option value="tilldate"
                      >Till Date</ion-select-option
                    >
                    <ion-select-option value="tillcount"
                      >Till Count</ion-select-option
                    >
                  </ion-select>
  
                  <ion-list v-if="repeatingTill == 'tilldate'">
                    <ion-item>
                      <ion-label>Choose date/time</ion-label>
                      <ion-datetime-button
                        datetime="datetime"
                      ></ion-datetime-button>
                      <ion-modal :keep-contents-mounted="true">
                        <ion-datetime id="datetime"></ion-datetime>
                      </ion-modal>
                    </ion-item>
                  </ion-list>
  
                  <ion-list v-if="repeatingTill == 'tillcount'">
                    <ion-item>
                      <ion-input
                        type="number"
                        labelPlacement="floating"
                        value="3"
                      >
                        <div slot="label">
                          <ion-text color="">Count</ion-text>
                        </div>
                      </ion-input>
                    </ion-item>
                  </ion-list>
                </ion-item>
              </ion-list>
            </ion-item>
            <!-- if custom option selected, show another form with all details -->
          </ion-list>
        </ion-content>
        
      </ion-modal>

      <!-- Preset Habits Modal -->
      <ion-modal :is-open="isOpenPreset">
        <ion-header>
          <ion-toolbar>
            <ion-buttons slot="start">
              <ion-button @click="setOpenPreset(false)">Cancel</ion-button>
            </ion-buttons>
            <ion-title></ion-title>
            <ion-buttons slot="end">
              <ion-button :strong="true">Confirm</ion-button>
            </ion-buttons>
          </ion-toolbar>
        </ion-header>

        <ion-content class="ion-padding">
            <p>Preset hABIT mODAL</p>
            <p>id: {{ habit_information.id }}</p>
        </ion-content>
        
      </ion-modal>


    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonText,
  IonPage,
  IonList,
  IonDatetimeButton,
  IonDatetime,
  IonCheckbox,
  IonGrid,
  IonRow,
  IonCol,
  IonButtons,
  IonButton,
  IonModal,
  IonHeader,
  IonContent,
  IonToolbar,
  IonTitle,
  IonItem,
  IonInput,
  IonLabel,
  IonIcon,
  IonSelect,
  IonSelectOption,
  IonListHeader,
  IonCardTitle,
  IonCardSubtitle,
  IonCardHeader,
  IonCard,
  IonTextarea,
  

} from "@ionic/vue";
import { addCircleOutline, batteryCharging, body, book, people, star } from "ionicons/icons";

import { OverlayEventDetail } from "@ionic/core/components";
import HabitModal  from "@/components/HabitModal.vue";

import { ref } from "vue";

//Habit Variables
const frequency = ref("Daily");
const repeatingFrequency = ref("Day");
const repeatEveryVal = ref(1);
const repeatingTill = ref("forever");

const habit_information = ref({
  id: "",
  title: "",
  description: "",
  start_date: "",
  end_date: "",
  frequency: "",
  repeating_frequency: "",
  repeat_every_val: 0,
  repeating_till: "",
});

//Modal Variables 
//1. Custom Habit Modal
const isOpen = ref(false);
const setOpen = (open: boolean) => (isOpen.value = open);
//2. Preset Habit Modal
const isOpenPreset = ref(false);
const setOpenPreset = (open: boolean, preset_id: string = "0") => {
  isOpenPreset.value = open;
  habit_information.value.id = preset_id;
};


</script>
