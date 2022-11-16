<template>
    <div id = "body">
        <!-- <img id="titulo" src="https://upload.wikimedia.org/wikipedia/commons/d/d6/Rick_and_Morty_title_card_%28cropped%29.png" alt=""> -->
        <h1>The Rick and Morty Characters</h1>
        <input type="text">
        <div class="container">
                <div v-for="character in characters.results" :key="character.id" class="individual">
                    <img :src = "character.image" alt=""/>
                    <div class="infowrap">
                        <!-- <h2 @click="openCharacter(character.id)"> NAME: {{ character.name }}</h2> -->
                        <router-link :to="{name: 'character', params: {id: character.id}}"><h2>{{character.name}}</h2></router-link> 
                        <p>
                            <span class="green" id="status" v-if="character.status== 'Alive'"></span>
                            <span class="red" id="status" v-else-if="character.status== 'Dead'"></span>
                            {{ character.status }}
                        </p> 
                        <p>Species: {{ character.species }}</p> 
                        <p>Gender: {{ character.gender }}</p>
                </div>
            </div>
        </div>
        <button id="prev-button" @click="previous == null ? callingAPI(previous) : ''">Previous</button>
        <button id="next-button" @click=" callingAPI(next)">Next</button>
    </div>
</template>

<script>
// import { addListener } from 'process'

export default{
    name: "rickAndMorty",
    data(){
        return{
            characters: [],
            next: '',
            previous: '',
        }
    },
    methods: {
        callingAPI(url) {
            fetch(url).then(res => res.json().then((data) => {
                this.characters = data
                this.next = data.info.next
                this.previous = data.info.prev
            }))
        },
        // openCharacter(id){
        //     this.$router.push(`/character/${id}`)
        // }
    },
    mounted() {
        this.callingAPI(`https://rickandmortyapi.com/api/character`)
    }
    
}
</script>

<style scoped>
.individual{
    background-color: rgb(97, 93, 93);
    margin: 10px;
    width: 45vw;
    height: 40vh;
    font-size: 20px;
    display: flex;
    border-radius: 10px;
    padding: 1px;
    font-size: 25px;
}
.infowrap{
    margin-right:0;
    padding: 0;
}
div{
    display:inline-block;
    justify-content: space-around;
    color: white;
}
div>img{
    display: block;
    align-content: left;
    justify-items: left;
    height: inherit;
    border-radius: 10px;
    margin-right: 50px;
}
.container{
    display: flex;
    flex-wrap: wrap;
}
#body{
    background-color: black;
    margin: 0;
    padding: 0;
}
#status{
    height: 10px;
    width: 10px;
    border-radius: 50%;
    display: inline-block;
}
.green{
    background-color: green;
}
.red{
    background-color: red;
}
button{
    display: inline-block;
    margin: 20px;
    padding: 20px;
    background-color: rgb(58, 128, 0);
}
h2 :hover(){
    font-size: 30px;
    color: yellowgreen;
}
a{
    text-decoration: none;
    color: white;
}
p{
    text-align: right;
}
titulo{
    width: 100vw;
}
</style>