<template>
<div class="card">
    <div class="user-box">
        <button class="random-quote-button" v-on:click="getRandomQuote()">quote of the day</button>
    </div>
    <div class="quote-container">
        <div class="quote">
            <p>"{{data.en}}"</p>
            <div class="author">
                <p> {{data.author}}</p>
            </div>
        </div>
    </div>
</div>   
</template>


<script>    
import axios from "axios"

export default {
    data() {
        return {
            data:[],
        }
    },
    methods: {
        getRandomQuote(){
            axios.get('https://programming-quotes-api.herokuapp.com/quotes/random')
            .then((response) => {
                console.log(response.data)
                this.data=response.data
            })
            .catch((err)=> console.log(err))
        },
    }
}
</script>


<style scoped>



.card{
display:grid;
grid-template-columns: 1fr 2fr;
grid-template-rows: 1fr 2fr;
animation: down 2s cubic-bezier(.39, 0, .38, 1) .2s;
column-gap:10px;
border-radius:3px;
}
@media ( max-width: 1000px ) {
.card {
    display:flex;
    flex-direction: column;
    height: 400px;
    /* grid-template-columns: 1fr;
    grid-template-rows:1fr; */
}

}


.user-box{
    background-color:white;
    grid-auto-columns: 1/2;
    text-align: center;
    padding:35px;
    border-top-right-radius: 10px;
    border-top-left-radius: 10px;
}

.random-quote-button{
background-color:black;
color:aliceblue;
width:250px;
border: 1px solid black;
}
.quote-container{
    grid-column: 2/2;
    grid-row:2/2;
    background-color:white;
    border-bottom-right-radius: 10px;
    border-bottom-left-radius: 10px;
    text-align: center;
    padding:10px;
}

.quote {
    display:flex;
    flex-direction: column;
    justify-content: center;
    text-align: center;
    /* padding:25px; */
    /* grid-column:2/2;
    grid-row:1;
    background-color:white;
    margin:auto;
    width:75%;
    float:right; */
    /* justify-content: center; */
}

.author{
font-style: italic;
padding-left:400px;
}


</style>
