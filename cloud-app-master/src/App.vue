<script setup>
import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>
    <div>

        <div class="relative overflow-x-auto">
            <div>
                <div class="space-x-2">
                    <span>name</span>
                    <input type="text" v-model="name">
                </div>
                <div class="space-x-2">
                    <span>Platform</span>
                    <input type="text" v-model="platform">
                </div>
                <div class="space-x-2">
                    <span>year</span>
                    <input type="text" v-model="year">
                </div>
                <div class="space-x-2">
                    <span>genre</span>
                    <input type="text" v-model="genre">
                </div>
                <div class="space-x-2">
                    <span>Publisher</span>
                    <input type="text" v-model="publisher">
                </div>
                <div class="space-x-2">
                    <span>NA</span>
                    <input type="text" v-model="na">
                </div>
                <div class="space-x-2">
                    <span>EU</span>
                    <input type="text" v-model="eu">
                </div>
                <div class="space-x-2">
                    <span>JP</span>
                    <input type="text" v-model="jp">
                </div>
                <div class="space-x-2">
                    <span>Other</span>
                    <input type="text" v-model="other">
                </div>
                <div class="space-x-2">
                    <span>Global</span>
                    <input type="text" v-model="global">
                </div>

                <button @click="postOption">
                    Submit POST!
                </button>




            </div>
            <div class="my-4">
                <input v-model="searchbar" class="mr-4">

                <button @click="getOption">
                    Kliknij do filtra
                </button>
            </div>

            <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                    <tr>
                        <th scope="col" class="px-6 py-3">
                            Rank
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Name
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Platform
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Year
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Genre
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Publisher
                        </th>
                        <th scope="col" class="px-6 py-3">
                            NA_Sales
                        </th>
                        <th scope="col" class="px-6 py-3">
                            EU_Sales
                        </th>
                        <th scope="col" class="px-6 py-3">
                            JP_Sales
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Other_Sales
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Global Sales
                        </th>

                    </tr>
                </thead>
                <tbody>
                    <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700" v-for="game in games"
                        v-bind:key="game.Name">
                        <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            {{ game.id }}
                        </th>
                        <td class="px-6 py-4">
                            {{ game.Name }}
                        </td>
                        <td class="px-6 py-4">
                            {{ game.Platform }}
                        </td>
                        <td class="px-6 py-4">
                            {{ game.Year }}
                        </td>
                        <td class="px-6 py-4">
                            {{ game.Genre }}
                        </td>
                        <td class="px-6 py-4">
                            {{ game.Publisher }}
                        </td>
                        <td class="px-6 py-4">
                            {{ game.NA_Sales }}
                        </td>
                        <td class="px-6 py-4">
                            {{ game.EU_Sales }}
                        </td>
                        <td class="px-6 py-4">
                            {{ game.JP_Sales }}
                        </td>
                        <td class="px-6 py-4">
                            {{ game.Other_Sales }}
                        </td>
                        <td class="px-6 py-4">
                            {{ game.Global_Sales }}
                        </td>
                        <button @click="putOption(game.id)">
                            Submit PUT!
                        </button>
                    </tr>

                </tbody>
            </table>

        </div>

    </div>
</template>

<script>
import { ref } from "vue";
import axios from 'axios'

export default {

    data() {
        return {
            games: [],
            searchbar: '',
            name: '',
            platform: '',
            year: '',
            genre: '',
            publisher: '',
            na: '',
            eu: '',
            jp: '',
            other: '',
            global: '',
            id: ''

        }
    },
    created() {
        axios.get('http://localhost:8000/games', {
            'Content-Type': 'application/json'
        })
            .then(response => {
                this.games = response.data
            })

    },
    methods: {
        getOption() {
            this.games = []
            axios.get('http://localhost:8000/games/' + this.searchbar)
                .then(response => {
                    this.games = response.data

                })
        },
        postOption() {
            this.games = []
            axios.post('http://localhost:8000/games', {
                Name: this.name,
                Platform: this.platform,
                Year: this.year,
                Genre: this.genre,
                Publisher: this.publisher,
                NA_Sales: this.na,
                EU_Sales: this.eu,
                JP_Sales: this.jp,
                Other_Sales: this.other,
                Global_Sales: this.global
            })
                .then(response => {
                    this.games = response.data
                })
        },
        putOption(ID) {
            this.games = []
            axios.put('http://localhost:8000/games', {
                Name: this.name,
                Platform: this.platform,
                Year: this.year,
                Genre: this.genre,
                Publisher: this.publisher,
                NA_Sales: this.na,
                EU_Sales: this.eu,
                JP_Sales: this.jp,
                Other_Sales: this.other,
                Global_Sales: this.global,
                id: ID
            })
            .then(response => {
                this.games = response.data
                location.reload()
            })
        }
    }
}
</script>

<style scoped>
.logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
}

.logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
    filter: drop-shadow(0 0 2em #42b883aa);
}
</style>


