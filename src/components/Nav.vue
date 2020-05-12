<template>
   <nav>
    <div class="nav-wrapper">
      <a href="#" class="brand-logo">VS</a>
      <ul class="right">
        <li @click="refresh"><a>Refresh</a></li>
        <!-- <li @click="testSort"><a>testSort</a></li> -->
        <li @click="bubbleSort"><a>bubbleSort</a></li>
        <li @click="selectSort"><a>selectSort</a></li>
        <li @click="insertionSort"><a>insertionSort</a></li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
    methods:{
        refresh(){
            this.$root.$emit('refresh')
        },
        bubbleSort(){
            this.$root.$emit('bubbleSort')
        },
        selectSort(){
            this.$root.$emit('selectSort')
        },
        insertionSort(){
            this.$root.$emit('insertionSort')
        },
        testSort(){
            this.$root.$emit('testSort')
        },

    }

}
</script>

<style>

</style>