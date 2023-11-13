<template>
    <div class="movements">
      <h2 class="title">Historial</h2>
      <div class="constent">
        <MovementV v-for="{id,title,description,amount} in movements" 
          :key="id" 
          :title="title"
          :description="description"
          :amount="amount"
          @remove="remove"
          >
        </MovementV>
      </div>
    </div>
</template>

<script setup>
import { toRefs,defineProps,defineEmits } from 'vue';
import MovementV from './MovementV.vue';
const props=defineProps({
  movements:{
    type:Array,
    default:()=>[]
  }
})
const {movements}=toRefs(props)
console.log(movements.value)
const emit=defineEmits(["remove"])
const remove=(id)=>{
  console.log("removing element in process",id)
  emit("remove",id)
}

</script>

<style scoped>
.movements {
  max-height: 100%;
  padding: 0 8px;
  margin-bottom: 14px;
}

.title {
  margin: 8px 16px 24px 16px;
  color: var(--brand-blue);
}

.content {
  max-height: 68vh;
  display: flex;
  flex-direction: column;
  gap: 8px;
  overflow-y: scroll;
}
</style>