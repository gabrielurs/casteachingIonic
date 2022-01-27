<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-menu-button color="primary"></ion-menu-button>
        </ion-buttons>
        <ion-title>{{ video.title}}</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Video {{ $route.params.id }}</ion-title>
        </ion-toolbar>
      </ion-header>

      <div id="container">
        <iframe id="video" :src="video.url" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        <ion-card>
          <ion-card-header>
            <ion-card-title>{{ video.title}}</ion-card-title>
            <ion-card-subtitle>{{ video.published_at}}</ion-card-subtitle>
          </ion-card-header>

          <ion-card-content>
            {{ video.description}}
          </ion-card-content>
        </ion-card>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import casteaching from '@acacha/casteaching'
import {
  IonButtons,
  IonCardHeader,
  IonCard,
  IonCardSubtitle,
  IonCardTitle,
  IonCardContent,
  IonContent,
  IonHeader,
  IonMenuButton,
  IonPage,
  IonTitle,
  IonToolbar
} from '@ionic/vue';

export default {
  name: 'Video',
  components: {
    IonButtons,
    IonContent,
    IonHeader,
    IonMenuButton,
    IonPage,
    IonTitle,
    IonToolbar,
    IonCardHeader,
    IonCardTitle,
    IonCardSubtitle,
    IonCardContent,
    IonCard,
  },
  data(){
    return{
      video: {
      }
    }
  },
  async created() {
    const api = casteaching({baseUrl: 'https://casteaching.gabriel.alumnedam.me/api'})
    api.setToken("gaVpc0snoMsdM5w6aaiNu2DMLPxipTYB6mKdfUaT")
    this.video = await api.video.show(1);
  }
}
</script>

<style scoped>

#video {
  width:100%;
  height:70vh;
}

</style>