<template>
    <div>
       <svg 
        @touchstart="tap"
        @touchmove="tap"
        @touchend="untap"
        view-box="0,0 300,200">
        <line 
            stroke="#c4c4c4"
            stroke-width="3"
            x1="0"
            :y1="zero"
            x2="300"
            :y2="zero"
        ></line>
        <polyline
            fill="none"
            stroke="#0689B0"
            stroke-width="2"
            :points="points"
        />
        <line
        v-show="showpointer"
        stroke-width="2"
        stroke="#04b500"
        :x1="pointer"
        :x2="pointer"
        y1="0"
        y2="200"
        ></line>
    </svg>       
    <p>Ultimos 30 días</p>
    <div>{{ amounts }}</div>
</div>
</template>
<script setup>
import { ref,toRefs,defineProps, computed,defineEmits,watch, } from 'vue';

const zero=()=>{
    return amountToPixels(0)
}
const props=defineProps({
    amounts:{
        type:Array,
        default:()=>[]
    }
})
const {amounts}=toRefs(props)
const amountToPixels=(amount)=>{
    const minX=Math.min(...amounts.value)
    const maxX=Math.max(...amounts.value)
    const amountAbs=amount+Math.abs(minX)
    const minmax=Math.abs(maxX)+Math.abs(minX)    
    return 200-((amountAbs*100)/minmax)*2
    
}
const points=computed(()=>{
    const totalPoints=amounts.value.length;
    return amounts.value.reduce((points,amount,i)=>{
        const x=(300/totalPoints)*(i+1)
        const y=amountToPixels(amount)
        return `${points} ${x},${y}`
    },`0,${amountToPixels(amounts.value.length?amounts.value[0]:0)}`)
    
    
})

const showpointer=ref(false)
const pointer=ref(0)
const emit=defineEmits(["select"])
watch(pointer,(value)=>{
    const index=Math.ceil(value/(300/amounts.value.length))
    if(index<0||index>=amounts.value.length) return;
    
    console.log(amounts.value[index])
    emit("select",amounts.value[index-1])

})
const tap=({target,touches})=>{
    showpointer.value=true
    const elementWidth=target.getBoundingClientRect().width;
    const elemenX=target.getBoundingClientRect().x;
    const touchX=touches[0].clientX;
    pointer.value=((touchX-elemenX)*300)/elementWidth
    

}
const untap=()=>{
    showpointer.value=false
}


</script>
<style scoped>
svg {
  width: 100%;
  height: 300px;  
}

p {
  text-align: center;
}
</style>