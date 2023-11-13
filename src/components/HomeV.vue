<template>  
  <LayoutV>
    <template #header>
        <HeaderV></HeaderV>
    </template>
    <template #resume>
        <Resume :label="'Ahorro Total'" :amount="amount" :totalAmount="totalAmount">
            <template #graphic>
              <GraphicV :amounts="amounts" @select="select"></GraphicV>
            </template>
            <template #action>
               <ActionV @create="create"></ActionV>
            </template>
        </Resume>
    </template>
    <template #movements>
        <Movements :movements="movements" @remove="remove"></Movements>
    </template>
  </LayoutV>
</template>

<script>
import HeaderV from './HeaderV.vue';
import LayoutV from './LayoutV.vue';
import Resume from './Resume/Index.vue'
import Movements from './Movements/Index.vue'
import ActionV from './ActionV.vue';
import GraphicV from './GraphicV.vue';

export default {
    name: "HomeV",
    components: { HeaderV, LayoutV, Resume, Movements, ActionV, GraphicV },
    data(){
      return{            
            amount:null,
            movements: [ ],
        }
    },computed:{
      amounts(){
        const lastDays= this.movements.filter((m)=>{
          const today=new Date()
          const oldDate=today.setDate(today.getDate()-30)
          return m.time>=oldDate
        }).map(m=>m.amount)

        return lastDays.map((m,i)=>{
          const lastmovements=lastDays.slice(0,i+1)
          return lastmovements.reduce((suma,mov)=>suma+mov,0)
        })
      },
      totalAmount(){
        return this.movements.reduce((suma,m)=>suma+m.amount,0)
      }
    },
    mounted(){
      const movements=JSON.parse(localStorage.getItem("movements"))
      if(Array.isArray(movements)){        
        this.movements=movements.map(m=>{
          return {...m,time:new Date(m.time)}
      });
      }
    },
    methods:{
      create(movement){
        this.movements.push(movement)

      },
      remove(id){        
        const index=this.movements.findIndex(m=>m.id===id)
        this.movements.splice(index,1)
        console.log("ID to remove:",id)
      },
      save(){
        localStorage.setItem("movements",JSON.stringify(this.movements))
      },
      select(el){
        console.log(el)
        this.amount=el
      }
      
    }
};
</script>
<style>
body {
  margin: 1px;
}
</style>
