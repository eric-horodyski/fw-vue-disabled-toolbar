<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="tertiary">
        <ion-title>Repro</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <h1>ion-button :disabled issue repro</h1>
      <p>
        When an ion-button is used on a toolbar that uses a computed color,
        and the ion-button is disabled via a computed(), the appearance of the ion-button doesn't get
        reset and continues to appear disabled.
      </p>
      <h2>Steps to repro</h2>
      <ul>
        <li>
          Observe that "Reset" button in ion-item and "Reset" button in
          ion-footer -> ion-toolbar are both enabled
        </li>
        <li>Tap "Increment count" once</li>
        <li>Observe that both "Reset" buttons are now displayed as disabled</li>
        <li>Tap "Increment count" button until count is 3</li>
        <li>
          Observe that "Reset" button in ion-item is once again displayed as
          enabled
        </li>
        <li>Expected: "Reset" button in footer is displayed as enabled</li>
        <li>
          Actual: "Reset" button in footer is displayed disabled, but is
          actually enabled
        </li>
      </ul>

      <ion-item-group>
        <ion-item>
          <ion-label>Current count is {{ count }}</ion-label>
          <ion-button slot="end" v-on:click="incrementCount">
            Increment count
          </ion-button>
        </ion-item>
        <ion-item>
          <ion-label>isDisabled? {{ isDisabled }}</ion-label>
        </ion-item>
        <ion-item-divider>
          <ion-label>Button in an ion-item</ion-label>
        </ion-item-divider>
        <ion-item color="dark">
          <ion-button :disabled="isDisabled" @click="handleClick">
            Reset
          </ion-button>
        </ion-item>
      </ion-item-group>

    </ion-content>
    <ion-footer>
      <ion-toolbar color="dark">
        <ion-buttons slot="end">
          <ion-button :disabled="isDisabled" @click="handleClick">
            Reset
          </ion-button>
        </ion-buttons>
      </ion-toolbar>
      <ion-toolbar></ion-toolbar>
    </ion-footer>
  </ion-page>
</template>

<script lang="ts">
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar, IonButtons, IonButton, IonItem, IonFooter, IonItemGroup, IonItemDivider, IonLabel } from '@ionic/vue';
import { computed, ref, defineComponent } from 'vue';

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonButtons,
    IonButton,
    IonItem,
    IonFooter,
    IonItemGroup,
    IonItemDivider,
    IonLabel
  },
  setup() {
    const count = ref(0);
    return {
      count,
      isDisabled: computed(() => count.value > 0 && count.value < 3),
      incrementCount: () => {
        count.value = count.value + 1;
      },
      saveToolbarColor: computed(() => {
        return "dark";
      }),
      handleClick: () => {
        count.value = 0;
      }
    };
  }

});
</script>

<style scoped>
#container {
  text-align: center;
  
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  
  color: #8c8c8c;
  
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>