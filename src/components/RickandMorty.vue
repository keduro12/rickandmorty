<template>
    <div>
        <h1 class="title">Rick and Morty</h1>

        <div class="container">
            <div class="btn">
                <button class="btButton" v-bind:disabled="this.page === 1" v-on:click="previous">Previous</button>
                <h2>{{this.page}}</h2>
                <button class="btButton" v-bind:disabled="this.page === 42" v-on:click="next">Next</button>
            </div>
            <div class="grid">
                <div v-for="(item, index) in items" :key="index">
                    <div class="item">
                        <h2>{{item.name}}</h2>
                        <img v-bind:src="item.image">
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>


<script>
    import {
        ref,
        computed
    } from 'vue'


    export default {
        data() {
            return {
                items: [],
                page: 1
            }
        },
        mounted() {
            this.traerDatos()
        },
        methods: {

            async traerDatos() {

                const response = await fetch("https://rickandmortyapi.com/api/character?page=" + this.page)
                const data = await response.json()
                this.items = data.results;
            },

            previous() {
                this.page--;
                this.traerDatos()
            },

            next() {
                this.page++;
                this.traerDatos()
            },


        },

        computed: {

        },
    }
</script>


<style scoped>
    .title {
        font-size: 2.7rem;
        font-weight: bolder;
        text-align: center;
    }

    .container {
        max-width: 1500px;
        margin: auto;
    }

    .grid {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: 1rem;
        margin-bottom: 10px;
    }

    .item {
        background: #5555;
        text-align: center;
        border-radius: 5px;
    }

    .item:hover{
        box-shadow: 0 2px 25px 0 rgb(203 203 203 / 50%)
    }

    .item img {
        border-radius: 10px 10px 0 0;
    }
/* 
    .item img:hover{
        box-shadow: -5px -10px 5px 5px #5555;
    } */

    .item h2 {
        margin-bottom: 8px;
    }

    .btn {
        display: flex;
        justify-content: center;
    }


    .btButton{
        margin-left: 200px;
        margin-right: 200px;
        margin-bottom: 10px;
        width: 150px;
        height: 30px;
        cursor: pointer;
        border-radius: 8px ;
    }

    .btButton:hover{
        background: #5555;
        color: #E4DAD8;
        border: none;

    }

    h2{
        margin: 0%;
    }
</style>