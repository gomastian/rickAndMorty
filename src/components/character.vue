<template>
    <div id = "body">
        <h1>The Rick and Morty Characters</h1>
        <div class="container">

                <div class="individual">
                    <img :src = "character.image" alt=""/>
                    <div class="infowrap">
                        <h2> NAME: {{ character.name }}</h2>
                        <p>
                            <span class="green" id="status" v-if="character.status== 'Alive'"></span>
                            <span class="red" id="status" v-else-if="character.status== 'Dead'"></span>
                            {{ character.status }}
                        </p> 
                        <p>Species: {{ character.species }}</p> 
                        <p>Gender: {{ character.gender }}</p>
                        <p> {{ character.type }}</p>
                </div>
            </div>
        </div>

    </div>
</template>

<script>

export default{
    name: "character",
    data(){
        return{
            character: {},
           
        }
    },
    methods: {
        callingAPI(url) {
            fetch(url).then(res => res.json().then((data) => {
                this.character = data
                
            }))
        }
    },
    mounted() {
        this.callingAPI(`https://rickandmortyapi.com/api/character/${this.$route.params.id}`)
    }
    
}
</script>

<style scoped>
.individual{
    background-color: #aaa;
    margin: 10px;
    width: 45vw;
    height: 40vh;
    font-size: 20px;
    text-align: right;
    display: flex;
    justify-content: left;
    border-radius: 10px;
    padding: 1px;

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
h2{
    font-size: 25px;
}
p{
    text-align: right;
}
</style>