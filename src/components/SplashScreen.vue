<template>
    <div class="splashscreen">
        <img src="../assets/cashflow-icon.svg" alt="cash-flow-icon"/>
        <h1><span>Splash</span><splash>Screen</splash></h1>
    </div>
</template>
<script>
export default{
   name: 'SplashScreen'
};
</script>
<style scoped>
.splashscreen {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}
h1 {
  color: var(--brand-blue);
}
h1 span {
  color: var(--brand-green);
}
</style>