<template>
 <v-card class="mx-auto" style="width: 300px; height: 100px;" :class="bg" :prepend-icon="ic">
  <template v-slot:title>
   {{ this.title }}
  </template>
 </v-card>
</template>

<script>
export default {
 props: {
  title: String,
  bg: String,
  ic: String,
 }
}
</script>
