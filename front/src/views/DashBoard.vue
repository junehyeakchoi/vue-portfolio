<template>
  <div class="text-h4 pa-6">MVP🥇</div>
  <v-container fluid>
    <v-row>
      <v-col>
        <my-card :title="$route.query.mvp" bg="bg-cyan-lighten-4" ic="mdi-baseball-diamond"></my-card>
      </v-col>
      <v-col>
        <my-card :title="$route.query.homerun" bg="bg-orange-lighten-4" ic="mdi-baseball-bat"></my-card>
      </v-col>
      <v-col>
        <my-card :title="$route.query.hit" bg="bg-grey-lighten-2" ic="mdi-baseball"></my-card>
      </v-col>
      <v-col>
        <my-card :title="$route.query.stolenbase" bg="bg-lime-lighten-3" ic="mdi-basketball"></my-card>
      </v-col>
    </v-row>
    <div class="text-h4 mt-5">우승🏆</div>
    <v-img class="align-end text-white" height="300" :src="`/${$route.query.year}.PNG`" width="auto">

    </v-img>

  </v-container>
</template>
<script >
import MyCard from '@/components/MyCard.vue';

export default {
  components: {
    MyCard,
  },
}
</script>
