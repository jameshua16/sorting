<template>
    <div class="app">
        <div v-for="index in amount" :key="index">
            <Div :length="divLength[index-1]" :ref="`div${index-1}`"/>
        </div>
    </div>

</template>

<script>
    import Div from './Div.vue'
    export default {
        name: 'Sort',
        data() {
            return {amount: 15, divLength: [], ret: {}}
        },
        components: {
            Div

        },
        methods: {
            hltDiv(id, color) {
                //console.log(this.$refs["div"+id][0])
                this.$refs["div" + id][0].$el.classList.add("highlight" + color)
                var vm = this
                setTimeout(function () {
                    vm.$refs["div" + id][0].$el.classList.remove("highlight" + color)
                }, 80)
            },
            init() {
                for (var i = 0; i < this.amount; i++) {
                    this.$set(this.divLength, i, Math.floor(Math.random() * 300))
                }
                console.log(this.divLength)
            },
            swap(num1, num2, arrayA) {
                let temp = arrayA[num1] - arrayA[num2]
                arrayA[num1] = arrayA[num1] - temp
                arrayA[num2] = arrayA[num2] + temp
            },
            swapAndSet(num1, num2, arrayA) {
                let temp = arrayA[num1] - arrayA[num2]
                this.$set(arrayA, num1, arrayA[num1] - temp)
                this.$set(arrayA, num2, arrayA[num2] + temp)
            },
            bubbleSort() {
                let count = 0
                var temp = this.divLength.slice(0)
                for (let i = 0; i < this.amount - 1; i++) {
                    for (let j = 0; j < this.amount - i - 1; j++) {
                        count++
                        if (temp[j] > temp[j + 1]) {
                            this.ret[count] = {
                                items: [
                                    j, j + 1
                                ],
                                hlt: 1
                            }
                            this.swap(j, j + 1, temp)

                        } else {
                            this.ret[count] = {
                                items: [
                                    j, j + 1
                                ],
                                hlt: 0
                            }
                        }

                    }
                }
                for (let key in this.ret) {
                    setTimeout(() => {
                        if (this.ret[key].hlt == "1") {
                            //this.hltDiv(this.ret[key].items[0],"Pink")
                            this.hltDiv(this.ret[key].items[1], "Pink")
                            this.swapAndSet(this.ret[key].items[0], this.ret[key].items[1], this.divLength)
                        } else {
                            //this.hltDiv(this.ret[key].items[0],"Blue")
                            this.hltDiv(this.ret[key].items[1], "Blue")

                        }
                        console.log(this.ret[key])
                    }, 100 * key)

                }

            },
            selectSort() {
                //let count = 0
                var temp = this.divLength.slice(0)
                for (let i = 0; i < this.amount-1; i++) {
                    let min_index = i
                    this.ret[i]=[]
                    for (let j = i + 1; j < this.amount; j++) {
                        //count++
                            if (temp[j] < temp[min_index]) {
                                
                                this.ret[i].push(["compare1",j,min_index])
                                min_index = j
                            }
                            else{
                                this.ret[i].push(["compare2",j,min_index])
                            }
                            
                    }
                    this.ret[i].push(["swap",i,min_index])
                    this.swap(min_index,i,temp)
                }
                let count = 0
                for (let key in this.ret) {
                   this.ret[key].forEach((a)=>{
                       count++
                        //console.log(a.index)
                        setTimeout(() => {
                            if(a[0]=="compare1"){
                                this.hltDiv(a[1],"Pink")
                                this.hltDiv(a[2], "Pink")
                            }
                            else if(a[0]=="compare2"){
                                this.hltDiv(a[1],"Blue")
                                this.hltDiv(a[2], "Blue")
                            }
                            else if(a[0]=="swap"){
                                this.swapAndSet(a[1], a[2], this.divLength)
                            }
                        }, 100 * count)
                   })
                    

                }
            },
            insertionSort() {
                let count = 0
                var temp = this.divLength.slice(0)
                for (let i = 1; i <= this.amount; i++) {
                    for (var j = i - 1; j>=0; j--) {
                        count++
                        if(temp[j]<temp[j-1]){
                            this.ret[count] = {
                                items: [
                                    j, j - 1
                                ],
                                hlt: 1
                            }
                            this.swap(j,j-1,temp)
                        }else{
                            this.ret[count] = {
                                items: [
                                    j, j - 1
                                ],
                                hlt: 0
                            }
                        }
                    }

                }
                //console.log(temp)
                for (let key in this.ret) {
                    setTimeout(() => {
                        if (this.ret[key].hlt == "1") {
                            this.hltDiv(this.ret[key].items[0],"Pink")
                            this.hltDiv(this.ret[key].items[1], "Pink")
                            this.swapAndSet(this.ret[key].items[0], this.ret[key].items[1], this.divLength)
                        } else {
                            this.hltDiv(this.ret[key].items[0],"Blue")
                            this.hltDiv(this.ret[key].items[1], "Blue")

                        }
                    }, 100 * key)

                }
            }
        },

        created() {
            this.init()
        },
        mounted() {
            this
                .$root
                .$on('refresh', () => {
                    this.init()
                })
            this
                .$root
                .$on('bubbleSort', () => {
                    this.bubbleSort()
                })
            this
                .$root
                .$on('selectSort', () => {
                    this.selectSort()
                })
            this
                .$root
                .$on('insertionSort', () => {
                    this.insertionSort()
                })
            //testSort
            this
                .$root
                .$on('testSort', () => {
                    this.testSort()
                })

        }

    }
</script>

<style>
    .app {
        display: flex;
        flex-direction: row;
    }
</style>