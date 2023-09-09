<template>
   <div>{{ $route.query }}</div>
   <v-card
            color="#385F73"
            theme="dark"
           >
            <v-card-title class="text-h5">
            {{ $route.query.mvp }}
           </v-card-title>
           <v-card-subtitle>    
            {{ $route.query.stolenbase }}
            
      </v-card-subtitle>
    </v-card>
     
  
</template>

<script setup>
</script>
