<template>  
  <LayoutV>
    <template #header>
        <HeaderV></HeaderV>
    </template>
    <template #resume>
        <Resume :label="'Ahorro Total'" :amount="amount" :totalAmount="1234567890">
            <template #graphic>
                graphic
            </template>
            <template #action>
                action
            </template>
        </Resume>
    </template>
    <template #movements>
        <Movements :movements="movements"></Movements>
    </template>
  </LayoutV>
</template>

<script>
import HeaderV from './HeaderV.vue';
import LayoutV from './LayoutV.vue';
import Resume from './Resume/Index.vue'
import Movements from './Movements/Index.vue'


export default {
    name: "HomeV",
    components: { HeaderV, LayoutV, Resume, Movements},
    data(){
        return{
            amount:null,
            movements: [
        {
          id: 1,
          title: "Movimiento",
          description: "Deposito de salario",
          amount: "1000",
        },
        {
          id: 2,
          title: "Movimiento 1",
          description: "Deposito de honorarios",
          amount: "500",
        },
        {
          id: 3,
          title: "Movimiento 3",
          description: "Comida",
          amount: "-100",
        },
        {
          id: 4,
          title: "Movimiento 4",
          description: "Colegiatura",
          amount: "1000",
        },
        {
          id: 5,
          title: "Movimiento 5",
          description: "Reparación equipo",
          amount: "1000",
        },
      ],
        }
    }
};
</script>
<style>
body {
  margin: 1px;
}
</style>
