<template>

  <ion-page>

    <ion-header>
      <ion-toolbar>
        <ion-title>Liste des potions</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">        
        <ion-toolbar>
          <ion-title size="large">Tab 3</ion-title>
        </ion-toolbar>
      </ion-header>
<!--
<pre>
Liste : {{liste}}
</pre>
-->
        <ion-list>
          <ion-item 
            v-for='potion in liste' 
            :key='potion.id' 
            :routerLink="'/potion/' + potion.id" :detail="false" class="list-item">
              <ion-icon :icon="wine" />
              &nbsp;{{potion.nom}}
          </ion-item>
        </ion-list>     

    </ion-content>
  </ion-page>

</template>

<script lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonList, IonIcon } from '@ionic/vue';
import { wine } from 'ionicons/icons';
import { defineComponent } from 'vue';

/* Import axios */
import axios from "axios";

export default defineComponent({
  data() {
    return {
      // Liste pour les villageois
      liste:[]
    }
  },

  /* montage du composant */
  mounted(){
    console.log("mounted");
    // Recherche des villageois
    axios
      .get("https://jsongaulois.jmfino.fr/listePotions.php")
      .then((response) => {
        console.log("reponse : ", response.data);
        this.liste = response.data;
        console.log("les batailles : ", this.liste);
    });
  },
    components: { 
    IonHeader, 
    IonToolbar, 
    IonTitle, 
    IonContent, 
    IonPage,
    IonItem, 
    IonList,
    IonIcon
  },
  setup() {
    return {
      wine
    }
  }


})
</script>


