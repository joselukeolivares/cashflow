<template>
  <Suspense>
    <template #default>
      <HomeV></HomeV>
    </template>  
    <template #fallback>
      <SplashScreen></SplashScreen>
    </template>
  </Suspense>
</template>

<script>
import HomeV from "@/components/HomeV.vue";
import SplashScreen from "./components/SplashScreen.vue";
import { defineAsyncComponent } from "vue";

export default {
  components: {
    HomeV:defineAsyncComponent(()=>{
       return new Promise((resolve,reject)=>{
        setTimeout(()=>{
          resolve(import("./components/HomeV.vue"))
        },2500)
      }).catch(e=>{
        console.log(e)
      })
    }),
    SplashScreen
},
};
</script>

<style>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}
* {
  --brand-green: #04b500;
  --brand-blue: #0689b0;
}
</style>
