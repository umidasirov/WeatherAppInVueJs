<script>
import axios from "axios";
export default {
  data(){
    return{
      city:'',
      error:"",
      info:null
    }
  },
  methods:{
    cls(){
      this.city=''
    },
    getWeather(){
      if ( this.city.trim().length < 2){
      this.error="Нужно название более одного символа!!!🚀🧒"

        return false
      }
      else {
        this.error = ""
      }
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=c3a632617a61cf98a3eeef8d4357bef2`)
          .then(res=>this.info = res.data)
    }
  },
  computed:{
    cityName(){
      return "городе " + '"' + this.city + '"'
    },
    showTemp(){
      return "Температура:" + this.info.main.temp
    },
    showFeelsLike(){
      return "Ощущантся как:" + this.info.main.feels_like
    },
    showMinTemp(){
      return "Минимальная Температура:" + this.info.main.temp_min
    },
    showMaxTemp(){
      return "Максимальная Температура:" + this.info.main.temp_max
    },
  }
}
</script>

<template>
<div class="wrapper">
  <h1 >Погода</h1>
  <p>Узнать погоды в {{city == "" ? "вашем городе" : cityName}} </p>
  <input placeholder="Введите город ..." type="text" v-model="city"><i @click="cls" class="fa-duotone fa-solid fa-xmark"></i><br>
  <button type="button" v-if="city != ''" @click="getWeather()">Получить погоду</button>
  <button class="disabled" type="button" disabled v-else>Введите название города</button>
  <p class="error">{{error}}</p>
  <div v-if="info!=null">
    {{showTemp}}<br>
    {{showFeelsLike}}<br>
    {{showMaxTemp}}<br>
    {{showMinTemp}}<br>
  </div>
</div>
</template>

<style scoped>
.error{
  color: blue;
}
.wrapper{
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  box-shadow: 15px 15px 15px 20px rgba(0, 0, 0, 0.15);
  text-align: center;
}
.wrapper h1{
  margin-top: 50px;
}
.wrapper p{
  margin-top: 20px;
}
.wrapper input{
  border: 0;
  color: white;
  padding: 5px 8px;
  outline: none;
  font-size: 14px;
  margin-top: 30px;
  background: transparent;
  border-bottom: 2px solid white;
}
.wrapper input::placeholder{
  color: aqua;
}
.wrapper button{
  padding: 4px 8px;
  color: white;
  background: transparent;
  border-radius: 5px;
  margin-top: 15px;
  border-color: white;
  cursor: pointer;
  transition: transform 400ms ease;
}
.wrapper button:hover{
  transform: scale(1.1) translateY(-5px);
}
.wrapper input:focus{
  border-bottom-color: aqua;
}
.disabled{
  cursor: no-drop !important;
}
.fa-solid{
  cursor: pointer;
  transition: transform 400ms ease;
}
.fa-solid:hover{
  transform: scale(1) translateY(-2px);
}
</style>
