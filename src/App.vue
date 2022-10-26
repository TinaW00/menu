<template>
  <v-app>
    
    <v-main>
      <HelloWorld/>
      <!-- <HintComponent/> -->
      <!-- <ResultSetUI/> -->
    </v-main>

   
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
// import HintComponent from './components/HintComponent';
// import ResultSetUI from './components/ResultSetUI';


export default {
  name: 'App',

  components: {
    HelloWorld,
    // HintComponent,
    // ResultSetUI,
  },

  data: () => ({
    //
  }),
};
</script>
