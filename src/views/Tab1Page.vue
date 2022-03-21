<template>

  <ion-page>

    <ion-header>
      <ion-toolbar>
        <ion-title>Liste des villageois</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">        
        <ion-toolbar>
          <ion-title size="large">Tab 1</ion-title>
        </ion-toolbar>
      </ion-header>
<!--
<pre>
Liste : {{liste}}
</pre>
-->
        <ion-list>
          <ion-item 
            v-for='villageois in liste' 
            :key='villageois.id' 
            :routerLink="'/villageois/' + villageois.id" :detail="false" class="list-item">
              <ion-thumbnail>
                <img :src='villageois.image' />
              </ion-thumbnail>
              &nbsp;{{villageois.nom}} {{villageois.laSpecialite.nom}}
          </ion-item>
        </ion-list>     

    </ion-content>
  </ion-page>

</template>

<script lang="ts">
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonItem, IonList, IonThumbnail } from '@ionic/vue';

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
      .get("https://jsongaulois.jmfino.fr/listeVillageois.php")
      .then((response) => {
        console.log("reponse : ", response.data);
        this.liste = response.data;
        console.log("les villageois : ", this.liste);
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
    IonThumbnail
  },


})
</script>
<style>
ion-page {
  --background: url('/src/img/fond cr.jpg') no-repeat 100% 100%;
}
</style>


