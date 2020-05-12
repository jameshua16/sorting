<template>
<div class="app"> 
    <div v-for="index in amount" :key="index">       
      <Div :length="divLength[index-1]" :ref="`div${index-1}`" />
    </div>
</div>
 
</template>

<script>
import Div from './Div.vue'
export default {
    name:'Sort',
    data(){
        return{
            amount:20,
            divLength:[]
        }
    },
    components:{
        Div

    },
 methods:{
    hltDiv(id,color){
        //console.log(this.$refs["div"+id][0])
        this.$refs["div"+id][0].$el.classList.add("highlight"+color)
        var vm = this
        setTimeout(function() { 
                    vm.$refs["div"+id][0].$el.classList.remove("highlight"+color)
                }, 150)
    },
    init(){
        for(var i=0;i<this.amount;i++){
            this.$set(this.divLength,i,Math.floor(Math.random()*300))
        }
        console.log(this.divLength)
    },
    swap(num1,num2,arrayA){
        let temp=arrayA[num1] - arrayA[num2]
        this.$set(arrayA, num1, arrayA[num1] - temp) 
        this.$set(arrayA, num2, arrayA[num2] + temp) 
    },
    bubbleSort(){
        let count = 0
        for(let i = 0;i<this.amount-1;i++){ 
            for(let j=0;j<this.amount-i-1;j++){
                count++
                var vm = this
                setTimeout(function() {
                    if(vm.divLength[j]>vm.divLength[j+1]){ 
                        vm.hltDiv(j,"Pink")
                        vm.hltDiv(j+1,"Pink") 
                        vm.swap(j,j+1,vm.divLength)                                            
                    }
                    else{
                        vm.hltDiv(j,"Blue")
                        vm.hltDiv(j+1,"Blue")
                    }
                }, 200*count)
            }
            
        }
    },
    selectSort(){
        let count = 0
        for(let i = 0;i<this.amount-1;i++){
            let min_index = i
            for(let j=i+1;j<this.amount;j++){
                count++
                var vm = this
                setTimeout(function() { 
                    if(vm.divLength[i]>vm.divLength[min_index]){ 
                        vm.hltDiv(i,"Pink")
                        vm.hltDiv(min_index,"Pink") 
                        vm.swap(min_index,i,vm.divLength)     
                    } else{
                            vm.hltDiv(j,"Blue")
                            vm.hltDiv(i,"Blue")  
                            if(vm.divLength[j]<vm.divLength[min_index]){ 
                                min_index = j    
                                }
                        }       
                    }, 200*count)
                }
            }
    },
    insertionSort(){
        //let count = 0
        for(let i = 1;i<this.amount;i++){
            let temp = this.divLength[i]
                var vm = this
                    for(var j = i-1;(j>=0 && vm.divLength[j]>temp);j--){
                        // vm.hltDiv(j,"Blue")
                        // vm.hltDiv(i,"Blue") 
                        vm.$set(vm.divLength, j+1, vm.divLength[j])
                    
                    
                    console.log(j)
                    }
                    vm.$set(vm.divLength, j+1, temp)
                    
                
        }
    }
},

    created(){      
        this.init()
    },
    mounted(){
        this.$root.$on('refresh',()=>{
            this.init()
        })
        this.$root.$on('bubbleSort',()=>{
            this.bubbleSort()
        })
        this.$root.$on('selectSort',()=>{
            this.selectSort()
        })
        this.$root.$on('insertionSort',()=>{
            this.insertionSort()
        })
        //testSort
        this.$root.$on('testSort',()=>{
            this.testSort()
        })
        
    }
 
}
</script>

<style>
.app{
    display: flex;
    flex-direction: row;
}

</style>