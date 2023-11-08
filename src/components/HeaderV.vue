<template>    
    <div class="header">
        <img @click=reload src="../assets/cashflow-icon.svg" alt="logo">
        <h1><span>CashFlow</span></h1>
        <span/>
    </div>
</template>

<script>
export default{
    name:"HeaderV",
    methods:{
        reload(){
            location.reload()
        }
    }
}
</script>
<!--scoped in style to indicate only apply this style to this component-->
<style scoped>
.header {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100vw;
}
img,
span {
  width: 48px;
}
h1 {
  font-size: 1.4rem;
  color: var(--brand-blue);
}
h1 span {
  color: var(--brand-green);
}
</style>