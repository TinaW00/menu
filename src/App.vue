<template>
  <v-app>
    
    <v-main>
      <HelloWorld/>
      <!-- <HintComponent/> -->
    </v-main>

   
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
// import HintCompnent from './components/HintComponent';


export default {
  name: 'App',

  components: {
    HelloWorld,
    // HintComponent,
  },

  data: () => ({
    //
  }),
};
</script>
