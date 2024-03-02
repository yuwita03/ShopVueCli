<template>
    <transition name="costum" enter-active-class="animated fadeInDown" leave-active-class="animated slideOutRight">
        <div v-if="sliderStatus">
          <div class="align-items-center mb-3" :class="sliderState">
            <label for="" class="font-weight-bold mr-2">Max</label>
            <input type="number" class="form-control mx-2" style="width: 60px; text-align: center;" v-model="maxAmount" @change="$emit('update:maximum', maxAmount)">
            <input type="range" name="" id="" class="custom-range" max="200" min="0" v-model="maxAmount" @input="$emit('update:maximum', maxAmount)">
          </div>
        </div>
    </transition>
</template>
<script>

export default{
    name:"price-slider",
    props: ["sliderStatus", "maximum"],
    data: function(){
        return {
            maxAmount: 50,
        }
    },
    computed:{
        sliderState: function () {
            return this.sliderStatus ? 'd-flex' : 'd-none';
        },
    }

}
</script>

<style>
.fade-enter, .fade-leave-to {
    opacity: 0;
}
.fade-enter-active, .fade-leave-active{
    transition: all 1s ease-in-out;
}
</style>