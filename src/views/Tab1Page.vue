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

      <ion-grid>
        <ion-row>
          <ion-col>
            <ion-button id="open-modal" expand="block" color="medium"
              >Create Custom Habit
              <ion-icon slot="end" :icon="addCircleOutline"></ion-icon
            ></ion-button>
          </ion-col>
        </ion-row>
      </ion-grid>

      <ion-list expand="block">
        <ion-list-header>
          <ion-label>Choose Preset Habits</ion-label>
        </ion-list-header>
        <ion-item>
          <ion-button expand="block" fill="outline">Sleep</ion-button>
        </ion-item>
        <ion-item>
          <ion-button expand="block" fill="outline">Exercise</ion-button>
        </ion-item>
        <ion-item>
          <ion-button expand="block" fill="outline">Eating</ion-button>
        </ion-item>
      </ion-list>

      <ion-modal ref="modal" trigger="open-modal" @willDismiss="onWillDismiss">
        <ion-header>
          <ion-toolbar>
            <ion-buttons slot="start">
              <ion-button @click="cancel()">Cancel</ion-button>
            </ion-buttons>
            <ion-title></ion-title>
            <ion-buttons slot="end">
              <ion-button :strong="true" @click="confirm()">Confirm</ion-button>
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
                    label="Repeat Frequency"
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
} from "@ionic/vue";
import { addCircleOutline } from "ionicons/icons";

import { OverlayEventDetail } from "@ionic/core/components";
import CustomHabitModal  from "@/components/CustomHabitModal.vue";

import { ref } from "vue";

const frequency = ref("Daily");
const repeatingFrequency = ref("Day");

const repeatEveryVal = ref(1);

const repeatingTill = ref("forever");

const message = ref(
  "This modal example uses triggers to automatically open a modal when the button is clicked."
);

const modal = ref();
const input = ref();

const cancel = () => modal.value.$el.dismiss(null, "cancel");

const confirm = () => {
  const name = input.value.$el.value;
  modal.value.$el.dismiss(name, "confirm");
};

const onWillDismiss = (ev: CustomEvent<OverlayEventDetail>) => {
  if (ev.detail.role === "confirm") {
    message.value = `Hello, ${ev.detail.data}!`;
  }
};
</script>
