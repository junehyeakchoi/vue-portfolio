<template>
  
  <v-navigation-drawer
    permanent
    theme="dark"
  >
    <v-list nav>
      <v-list-item title="BASEBALL" @click="moveHome"></v-list-item>
      <v-list-item v-for="(item, i) in yearList" :key="item" :title="item.year" :value="i" @click="select(item, $event)"></v-list-item>
    </v-list>
  </v-navigation-drawer>    
</template>
<script>
export default {
  methods: {
    select(item) {
      console.log(item);
      this.$router.push({name: 'DashBoard', query: item})
    },
    moveHome() {
      this.$router.push('/')
    }
  },
  data() {
    return {
      yearList: [{
        year: 2017,
        mvp: '노시환',
        homerun: '아니',
        stolenbase : "손아섭 " , 
        hit: "qqq" , 
      

      },
      {
        year: 2018,
        mvp: 'gkgk',
        homerun: '이대호',
        stolenbase : "응" ,
        hit: "www" ,

      },
      {
        year: 2019,
        mvp: 'dzzd',
        homerun: "ㅇㅇ",
        stolenbase : "sssd" ,
        hit: "rrr" ,
        
      },
      {
        year: 2020,
        mvp: 'dydy',
        homerun: "dddd", 
        stolenbase: "nnnnn" ,
        hit: "kkk" ,


      },
      {
        year: 2021,
        mvp: 'rkrk',
        homerun : "dsdsad",
        stolenbase : "ggg" ,
        hit: "ttt" ,

      },
      {
        year: 2022,
        mvp: 'nknknk',
        homerun : "hhhhh" ,
        stolenbase : "iiii" ,
        hit : "ppp",

      },
      {
        year: 2023,
        mvp : " rhleske ",
        homerun : "tttt",
        stolenbase: "kkkk" ,
        hit : "ooo" ,
      }
    ]
    }
  }
}
</script>

