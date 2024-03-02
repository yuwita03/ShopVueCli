<template>
    <transition-group name="fade" tag="div" enter-active-class="animated fadeInRight" leave-active-class="animated fadeOutRight">
        <div class="row d-flex mb-3 align-items-center" v-for="(item, index) in showItem" :key="index" :data-index="index">
            <div class="col-1 m-auto">
                <button class="btn btn-info" v-on:click="$emit('add', item)">+</button>
            </div>
            <div class="col-sm-4 align-items-center">
                <img :src="item.image" :alt="item.name" class="img-fluid d-block">
            </div>
            <div class="col">
                <h3 class="text-info">{{ item.name }}</h3>
                <p class="mb-0">{{ item.description }}</p>
                <div class="h5 float-right">
                <price :value="Number(item.price)"></price>
                </div>
            </div>
        </div>
    </transition-group>
</template>
<script>
    import Price from "./Price.vue"
    export default{
        name: "product-list",
        components:{
            Price
        },
        props: ["products", "maximum"],
        computed: {
            showItem: function(){
                let max = this.maximum;
                return this.products.filter(function(item){
                    // digunakan untuk mengambil bagian bilangan bulat dari suatu angka dengan menghilangkan bagian desimalnya
                    return Math.trunc(item.price) <= max;
                })
            }
        },
        methods: {
            before: function(el){
                el.className= 'd-none'
            },
            enter: function(el){
                var delay = el.dataset.index * 100;
                setTimeout(() => {
                    el.className = 'row d-flex mb-3 align-items-center animated fadeInRight'
                }, delay);
            },
            leave: function(el){
                var delay = el.dataset.index * 100;
                setTimeout(() => {
                    el.className = 'row d-flex mb-3 align-items-center animated fadeOutRight'
                }, delay);
            },
        }
    }
</script>