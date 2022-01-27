<template>
  <ion-content>
  <ion-refresher slot="fixed" @ionRefresh="refresh" id="refresher">
    <ion-refresher-content></ion-refresher-content>
  </ion-refresher>
  <ion-list>
    <ion-list-header> Videos </ion-list-header>

    <ion-item v-for="video in videos" :key="video.id">
      <ion-avatar slot="start">
        <img src="https://via.placeholder.com/80" />
      </ion-avatar>
      <ion-label>
        <h2>{{ video.title }}</h2>
        <p>{{video.description}}</p>
      </ion-label>
    </ion-item>
  </ion-list>
  </ion-content>
</template>

<script>
import {IonAvatar, IonContent, IonItem, IonLabel, IonList, IonListHeader, IonRefresherContent} from "@ionic/vue";
import casteaching from "@acacha/casteaching";
export default {
  name: "Videos",
  components:{
  IonList, IonItem, IonListHeader, IonAvatar,IonLabel,IonRefresherContent,IonContent
  },
  data(){
    return{
      videos:[],
      loading: true
    }
  },
  async created() {
    await this.fetchVideos();
    this.loading = false;
  },
  mounted() {
    this.refresher = document.getElementById('refresher');
  },
  methods:{
    async refresh(){
      await this.fetchVideos();
      this.refresher.complete();
      },
    async fetchVideos(){
      return this.videos = await casteaching({baseUrl:'https://casteaching.gabriel.alumnedam.me/api'}).videos();
    }
  }
}
</script>

<style scoped>

</style>