<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-back-button :text="getBackButtonText()" default-href="/"></ion-back-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" v-if="carte">
      <ion-grid>
        <ion-row>
          <ion-col>
            <ion-thumbnail>
              <ion-img :src="villageois.image"></ion-img>
            </ion-thumbnail>
          </ion-col>
          <ion-col>
            <ion-label class="ion-text-wrap">
              <h1>
                {{villageois.nom}}
                <br/>
                {{villageois.laSpecialite.nom}}</h1>                
              <h2><ion-note>{{villageois.leLieuHabitat.nom}}</ion-note></h2>
            </ion-label>
          </ion-col>
        </ion-row>
      </ion-grid>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { useRoute } from 'vue-router';
import { IonBackButton, IonButtons, IonContent, IonHeader, IonPage, IonToolbar, 
         IonThumbnail, IonImg, IonLabel, IonNote, IonGrid, IonRow, IonCol } from '@ionic/vue';
import { defineComponent } from 'vue';
/* Import axios */
import axios from "axios";

export default defineComponent({
  data() {
    return {
      getBackButtonText: () => {
        const win = window as any;
        const mode = win && win.Ionic && win.Ionic.mode;
        return mode === 'ios' ? 'Inbox' : '';
      },
      // Ajout id
      id : 0,
      // Ajout personne
      carte : null
    }
  },
  mounted(){
    const route = useRoute();
console.log("mounted fiche id route ", route.params.id);
    this.id = parseInt(route.params.id as string, 10);
console.log("mounted fiche", this.id);
    // Recherche du villageois concerné
    axios
      .get("https://api.clashroyale.com/v1/cards="+this.id)
      .then((response) => {
        this.carte = response.data;
        console.log("Carte : ", this.carte);
    });


  },  
  components: {
    IonBackButton,
    IonButtons,
    IonContent,
    IonHeader,
    IonPage,
    IonToolbar,  
    IonThumbnail,
    IonImg,
    IonLabel,
    IonNote,
    IonGrid,
    IonRow,
    IonCol

  },
});
</script>

<style scoped>

ion-thumbnail
{
  width:200px;
  height:280px; 
  img
  {
    width:auto !important;
    height:auto !important;
  }
}

ion-item {
  --inner-padding-end: 0;
  --background: transparent;
}

ion-label {
  margin-top: 12px;
  margin-bottom: 12px;
}

ion-item h2 {
  font-weight: 600;
}

ion-item .date {
  float: right;
  align-items: center;
  display: flex;
}

ion-item ion-icon {
  font-size: 42px;
  margin-right: 8px;
}

ion-item ion-note {
  font-size: 15px;
  margin-right: 12px;
  font-weight: normal;
}

h1 {
  margin: 0;
  font-weight: bold;
  font-size: 22px;
}

p {
  line-height: 22px;
}
</style>