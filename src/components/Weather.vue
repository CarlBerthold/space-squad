<template>
<div class="card">
    <div class="user-box">
        <div class="search-buttons">
            <input class="search-input" type="text" placeholder="enter city" v-model="search" v-on:change="getWeather()">
            <!-- <button class="search-button" type="button" v-on:click="getWeather()">search</button> -->
            <button class="space-squad" type="button" v-on:click="getSpaceSquadWeather()">space squad's weather</button>
        </div>
    </div>

    <div class="content">
        <div class="links">
            <div class="name">
                <h2>{{name}}</h2>
            </div>
            <div class="temp">
                <h1>{{temp}}°</h1>
            </div> 
                <img class="api-icon" v-bind:src="icon_url_1 + icon + icon_url_2"/>
        </div>
            <div class="rechts">
                <div class="windy">
                    <h3>{{wind}} km/h </h3>
                    <img class="icon" src="../assets/windyicon.png">
                </div>
                <div class="humidity">
                    <h3>{{humidity}} %</h3>
                    <img class="icon" src="../assets/humidityicon.png">
                </div>
                <div class="sunrise">
                    <h3>{{Unix_timestamp(sunrise)}} </h3>
                    <img class="icon" src="../assets/Aufgangicon.png">
                </div>
                <div class="sunset">
                    <h3>{{Unix_timestamp(sunset)}} </h3>
                    <img class="icon" src="../assets/sunseticon.png">
                </div>
            </div>
                <!-- <h3><span><img class="windyIcon" src="../assets/windyicon.png"></span>{{wind}} km/h</h3> -->
                <!-- <h3><span><img class="windyIcon" src="../assets/humidityicon.png"></span>{{humidity}} %</h3> -->
                <!-- <h3><span><img class="windyIcon" src="../assets/Aufgangicon.png"></span>at {{Unix_timestamp(sunrise)}}</h3> -->
                <!-- <h3><span><img class="windyIcon" src="../assets/sunseticon.png"></span>at {{Unix_timestamp(sunset)}}</h3> -->
            
    </div>
</div>
</template>


<script>
import axios from 'axios';



export default {
    name:'Weather',
    data(){
        return {
            search:null,
            lon:"",
            lat:"",
            windIcon:"",
            icon: "",
            temp:"",
            feelsLike:"",
            pressure:"",
            humidity:"",
            wind:"",
            clouds:"",
            dt:"",
            name:"",
            sunrise:"",
            sunset:"",
            icon_url_1: "",
            icon_url_2: "",
            timezone:"",
        }
    },
    methods: {
        getSpaceSquadWeather(){
    
        axios.get("https://api.openweathermap.org/data/2.5/weather?lat=52.468300&lon=13.389810&units=metric&appid=1bf2e86208f1c45e11ef23d56aeca143&lang=de")
        // axios.get(`http://api.openweathermap.org/geo/1.0/reverse?lat=${lat}&lon=${lon}&limit=1&appid=${API_key}`)
        .then((response)=> {
            console.log(response)
            this.lon=response.data.coord.lon
            this.lat=response.data.coord.lat

            this.icon=(response.data.weather[0].icon)

            this.temp=response.data.main.temp
            this.feelsLike=response.data.main.feels_like
            this.pressure=response.data.main.pressure
            this.humidity=response.data.main.humidity

            this.wind=response.data.wind.speed
            this.clouds=response.data.clouds.all
            this.dt=response.data.dt
            this.sunrise=response.data.sys.sunrise
            this.sunset=response.data.sys.sunset
            this.name=response.data.name
            this.timezone=response.data.timezone

            this.icon_url_1 = "https://openweathermap.org/img/wn/"
            this.icon_url_2 = "@2x.png"
        })
        .catch((err)=> console.log(err))
        },

        getWeather() {
            const API_key = "1bf2e86208f1c45e11ef23d56aeca143"
            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.search}&units=metric&appid=${API_key}&lang=de`)
            .then((response) => {
            console.log(response.data.timezone)
            this.lon=response.data.coord.lon
            this.lat=response.data.coord.lat
            this.icon=(response.data.weather[0].icon)
            this.temp=response.data.main.temp
            this.feelsLike=response.data.main.feels_like
            this.pressure=response.data.main.pressure
            this.humidity=response.data.main.humidity
            this.wind=response.data.wind.speed
            this.clouds=response.data.clouds.all
            this.dt=response.data.dt
            this.sunrise=response.data.sys.sunrise
            this.sunset=response.data.sys.sunset
            this.name=response.data.name
            this.timezone=response.data.timezone
            this.icon_url_1 = "https://openweathermap.org/img/wn/"
            this.icon_url_2 = "@2x.png"
            })
            .catch((err)=>console.log(err))
        },
        Unix_timestamp(t){
            if (!t){
                console.log("keine timestamp")
            } else {
        let dt = new Date(t*1000);
        let hr = dt.getHours();
        let m = "0" + dt.getMinutes();
        // let s = "0" + dt.getSeconds();
        let sunrise = hr+ ':' + m.substr(-2); 
        return sunrise
        }
        }
        
    }
}
</script>


<style scoped>
.card {
display:grid;
/* float:right; */
grid-template-columns: 1fr 1fr;
/* grid-auto-rows: minmax(100px, auto); */
/* overflow: hidden; */
animation: down 2s cubic-bezier(.39, 0, .38, 1) .2s;
column-gap:50px;
min-height:600px ;
/* background-color:white; */
}

@media ( max-width: 1000px ) {
.card {
    display:grid;
    grid-template-columns: 1fr;
    grid-template-rows:1fr 1fr;
}
}

@media (max-width:782px) {
    .card {
    display:flex;
    flex-direction:column;
    }


    
}

@media (max-width:650px) {
    .card {
        display:grid;
        grid-template-columns: 1fr;
        grid-template-rows: 1fr;
    }
    .content {
        display:grid;
        grid-template-rows: 1fr;
    }
    .rechts{
        grid-column: 1;
        grid-row:1;
    }
    .links{
        grid-column: 1;
        grid-row:1;
    }
}
.user-box{

    background-color:white;
    background-image: url(https://cdn.dribbble.com/users/1353252/screenshots/7430583/media/f456446ffc1c9a1608b94d6d136dbc0d.gif);
    background-size: 350px;
    background-repeat: no-repeat;
    background-position: bottom;
    border-radius:3px;

}
.search-buttons{
display:flex;
flex-direction: column;
margin:5%;
}
.search-input {
    text-align: center;
    background-color: rgb(255, 255, 255, 0.01);
    margin:5px;
    box-sizing:border-box;
    border:1px solid #f1f1f1;
    width: auto;
    height: 50px;
    border-radius: 3px;

}
.search-input:hover{
border:2px solid rgba(3, 169, 244, 0.8);
background-color:rgba(3, 169, 244, 0.5);
}

.space-squad{
    height:50px;
    margin:5px;
    border: 1px solid #f1f1f1;
    border-radius:3px;
    background-color: rgb(255, 255, 255, 0.01);
}
.space-squad:hover{
border:2px solid rgba(3, 169, 244, 0.8);
background-color:rgba(3, 169, 244, 0.5);
}
.content{
    text-align: center;
    background-color: white;
    display:grid;
    grid-template-columns: 1fr 2fr;
    /* grid-template-rows: 1fr 1fr 1fr 1fr; */
    column-gap: 50px;
    /* row-gap: 50px; */
    border-radius:3px;
    /* text-align: center;
    padding:25px; */

}

.links{
/* border:1px solid black; */
margin:auto;
grid-column: 1/2;

}
.name{
    width: 300px;
    /* float:top; */
    grid-column: 1/2;
    /* grid-row:1/4; */
}

.temp{
    width: 300px;
    /* margin:auto; */
    grid-column: 1/2;
    grid-row:2/4;

}


.rechts{
margin:auto;
grid-column: 2/2;

}
.windy{
    /* margin:auto; */
    /* grid-column: 2/2;
    grid-row:1/4; */
    height:fit-content;
}

.humidity{
        /* margin:auto; */
    height:fit-content;

    /* grid-column: 2/2;
    grid-row:2/4; */
}

.sunrise{
        /* margin:auto; */
    height:fit-content;

    /* grid-column: 2/2;
    grid-row:3/4; */
}

.sunset{
        /* margin:auto; */
    height:fit-content;
    /* grid-column: 2/2; */
    /* grid-row:4/4; */

}

.icon{
        /* margin:auto; */

    height: 50px;
    width: 50px;
}
.api-icon{
    /* border:1px solid black; */
    margin:auto;
    /* grid-column: 1/2;
    grid-row:4/4; */
    /* border:1px solid black;
    border-radius: 50%; */
}
</style>

