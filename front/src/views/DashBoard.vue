<template>
  <div class= "text-h4 mt- pa-"></div>
    <div>
    <v-text-field
      
      label="Seasons"
      :rules="rules"
      hide-details="auto"
    ></v-text-field>
    <v-text-field label="Player"></v-text-field>
  </div>
  <div v-if = "$route.query.year != 2023">
      <div class="text-h4
      
       pa-1">우승🏆</div>
      <v-img class="align-end text-white" height="300" :src="`/${$route.query.year}.PNG`" width="680px"/>
  </div>
  <div v-else>
    <div class="text-h4 mt-15 pa-1">현재 순위🏆</div>
    <v-img class="align-end text-white" height="300"  :src="`/${$route.query.year}.PNG`" width="auto"/>
    
  </div>
  <div class="text-h4 pa-5 mt-">MVP🥇</div>
  <v-container fluid>
    <v-row>
    
      <v-col>
        <my-card :title="$route.query.mvp" bg="bg-blue-lighten-4" ic="mdi-baseball-diamond"></my-card>
      </v-col>
      <v-col>
        <my-card :title="$route.query.homerun" bg="bg-blue-lighten-4" ic="mdi-baseball-bat"></my-card>
      </v-col>
      <v-col>
        <my-card :title="$route.query.hit" bg="bg-blue-lighten-4" ic="mdi-baseball"></my-card>
      </v-col>
      <v-col>
        <my-card :title="$route.query.stolenbase" bg="bg-blue-lighten-4" ic="mdi-basketball"></my-card>
      </v-col>
    </v-row>
    

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
