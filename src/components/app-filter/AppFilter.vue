<template >
    <div class="btn-group">
        <button class="btn " v-for="(item, index) in filterButtons" :key="index" type="button" @click="filterHandler(item.name)" :class="[filterName === item.name ? 'btn-dark' : 'btn-outline-dark']">{{ item.title }}</button>
        <!-- <button class="btn" type="button" @click="filterHandler('popular')" :class="[filterName === `popular` ? 'btn-dark' : 'btn-outline-dark']">Mashxur kinolar</button>
        <button class="btn" type="button" @click="filterHandler('mostViewers')" :class="[filterName === `mostViewers` ? 'btn-dark' : 'btn-outline-dark']">Eng ko'p ko'rilgan kinolar</button> -->
    </div>
</template>
<script>
export default {
    props: {
        updateFilterHandler:{
            type: Function,
            required : true
        },
        filterName: {
            type: String,
            required: true
        }
    },
    data(){
        return {
            filterButtons: [
                {
                    title: "Barcha kinolar",
                    name : "all"
                },
                {
                    title: "Mashxur kinolar",
                    name : "popular"
                },
                {
                    title: "Eng ko'p ko'rilgan kinolar",
                    name : "mostViewers"
                }
            ],
            filter: "all"
        }
    },
    methods:{
        filterHandler(filter){
            this.filter = filter
            this.updateFilterHandler(this.filter)
        }
    }
}
</script>
<style>
    
</style>