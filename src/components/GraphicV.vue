<template>
    <div>
       <svg view-box="0,0 300,200">
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
        stroke-width="2"
        stroke="#04b500"
        x1="200"
        x2="200"
        y1="0"
        y2="200"
        ></line>
       </svg>       
       <p>Ultimos 30 días</p>
    </div>
</template>
<script setup>
import { toRefs,defineProps, computed } from 'vue';


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
    },"0,50")


})


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