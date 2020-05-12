<template>
  <div class="divs" :style="{ height: length*3 + 'px' }" ref="div"></div>
</template>

<script>
export default {
    props: {
        length
      },
      data(){
          return{
                          
          }
      },  
    mounted(){
        this.$watch(
        () => {
            this.$refs.div.clientHeight
        },
      () => {
        console.log("changed")
      }
    )
           
    }
     
}
</script>

<style>
.divs{
    height: 300px;
    width: 80px;
    background-color: lightblue;
    margin:1px;
}
.highlightPink{
    background-color: lightpink;
}
.highlightBlue{
    background-color: #3a9fbf;
}

</style>