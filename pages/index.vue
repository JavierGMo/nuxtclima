<template>
  <div id="app" class="d-fx container-principal">
    <BaseAside 
        @update:updatedataweather="signalforchangestate($event)"
        @update:nextdaysweather="nextandtoday($event)"
        @update:cardsupdatedegree="fncchangecarddegree($event)"
        :datetoday="dateweather().format('ddd, D MMM')"
        :degreeChange="degreeChange"
        :statedegree="statedegree" />
    <BaseContent
        @update:degreessignal="degreeschange($event)"
        :datanextdays="datanextdays"
        :todayhightlights="todayhightlights"
        :dates="datesw"
        :auxchangecarddegree="auxchangecarddegree"/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import BaseAside from "../components/aside/BaseAside";
import BaseContent from "../components/content/BaseContent";
import moment from 'moment';

export default {
  name: 'App',
  components: {
    // HelloWorld,
    BaseAside,
    BaseContent,
  },
  head : {
    title : 'Clima | JGM',
    link: [
      {
        rel : 'stylesheet',
        href : "https://pro.fontawesome.com/releases/v5.10.0/css/all.css",
        integrity : "sha384-AYmEC3Yw5cVb3ZcuHtOA93w35dYTsvhLPVnYs9eStHfGJvOvKxVfELGroGkvsg+p",
        crossorigin : "anonymous"
      }
    ]
  },
  data(){
    return {
      datanextdays : undefined,
      todayhightlights : undefined,
      dateweather : moment,
      datesw : undefined,
      degreeChange : undefined,
      statedegree : true,
      auxchangecarddegree : true,
    }
  },
  methods : {
    nextandtoday : function(data){
      if(data){
        this.datesw = [];
        this.datanextdays = data.nextdays;
        this.todayhightlights = data.hightlights;
        // for (let i = 1; i < 6; i++)  this.datanextdays[i].date = this.calculateDate(i);
        for (let i = 1; i < 6; i++)  this.datesw.push(this.calculateDate(i));

        // console.log(this.datanextdays);
      }
    },
    calculateDate : function(adddays){
      return this.dateweather().add(adddays, 'days').format('ddd, D MMM')
    },
    degreeschange : function(degree){
        this.degreeChange = !degree;
    },
    signalforchangestate : function (signal) {
        this.statedegree = signal;
    },
    fncchangecarddegree : function(param){//Cambiar el los grados de las cards cuando esten en faren y volver al original
        this.auxchangecarddegree = param;
    }
  }
}
</script>

<style>
:root{
    --black-light: #212121;
    --blue-primary: #001233;
    --blue-secondary: #002855;
    /* --blue-light: #003459; */
    --white-light: #faf9f9;
    --gray-fifty: #979dac;
    --gray-light: #d3d3d3;
    --purple-primary: #3b28cc;
}
body{
    /* background-color: var(--black-light, #212121); */
    font-family: Arial, Helvetica, sans-serif;
    color: var(--gray-fifty);
    padding: 0;
    margin: 0;
}
/* img{
    width: 5%;
    height: 5%;
} */
/*Generals*/
button{
    cursor: pointer;
    background-color: var(--gray-light);
    border: none;
}
progress{
    appearance: none;
    overflow: hidden;
    border: none;
    border-radius: 20px;
    height: 10px;
}
.d-fx{
    display: flex;
}
.f-column{
    flex-direction: column;
}
.f-row{
    flex-direction: row;
}
.f-center{
    justify-content: center;
    align-items: center;
}
.f-between{
    justify-content: space-between;
}
.f-around{
    justify-content: space-around;
}
.f-fend{
    justify-content: flex-end;
}
.p-relative{
    position: relative;
}
.p-absolute{
    position: absolute;
}
.color-white-light{
    color: var(--white-light);
}
.color-gray-fifty{
    color: var(--gray-fifty);
}
.c-btn-rounded{
    border-radius: 100%;
    padding: 10px;
}
.container-principal{
    height: 100%;
}
#app{
  height: 100vh;
}
/*Bar search and info*/
.c-bar-search{
    /* background-color: rgba(3, 4, 94, 0.91); */
    background-color: var(--blue-secondary);
    width: 30%;
}
.contain-btns-search{
    padding: 1rem;
}

.containt-img-bar{
    /* width: 30%; */
}
.cont-deegree{
    margin-top: 1.5rem;
    margin-bottom: 2.5rem;
}
.weather-state-bar{
    margin-top: 1.5rem;
    margin-bottom: 2.5rem;
}
.txt-deegree-unit-bar{
    font-size: 7.5rem;
}
.txt-deegree-measure-bar{
    font-size: 3.5rem;
    font-weight: 100;
}
.weather-state-bar{
    font-size: 2.5rem;
    font-weight: 100;
}
.img-bar{
    width: 100%;
    height: 100%;
}
.container-result-place{
    padding: 1rem;
}
.c-btn-search-p{
    padding: 0.3rem 0.4rem;
}
.place-result{
    cursor: pointer;
    border: 1px solid var(--gray-fifty);
    margin-bottom: 1.3rem;
    padding: 0.1rem 0.4rem;
}
.ipt-search-place{
    background-color: transparent;
    border: 1px solid var(--gray-fifty);
    color: var(--white-light);
}
.btn-search-place{
    background-color: var(--purple-primary, #3b28cc);
    color: var(--white-light);
    /* padding: 1rem; */
}
.ipt-search-place, .btn-search-place{
    padding: 0.5rem;
    margin-bottom: 1.5rem;
}
.btn-close{
    color: var(--gray-light);
    background-color: transparent;
}

/*Data in cards*/
.c-contents-cards{
    flex-wrap: wrap;
}
.contain-cards-weather{
    flex-direction: column;
}
.c-btn-deegree{
    background-color: var(--gray-fifty);
}
.c-deegree-select{
    background-color: var(--gray-light);
    color: var(--blue-primary);
    /*Cambiar colores el seleccrionado debe de ser blanco*/
}
.c-content-units{
    padding: 1rem;
}
.c-content-units>div{
    margin-left: 0.5rem;
}
.c-content-weather{
    background-color: var(--blue-primary);
    padding-left: 0.4rem;
    width: 70%;
}
.c-card-w{
    width: 17%;
    height: 20vh;
    background-color: var(--blue-secondary);
    margin: 0 0.5rem;
}
.c-card-img-weat{
    width: 50%;
}

.c-card-general{
    background-color: var(--blue-secondary);
    height: auto;
    margin: 0 0.5rem;
    width: 15rem;
    margin-bottom: 1.5rem;
}
.txt-today-weather{
    font-size: 2.5rem;
    font-weight: 800;
}
.txt-complement-weather{
    font-size: 1.5rem;
    font-weight: 100;
}
.content-wind-status{
    margin-top: 1rem;
    margin-bottom: 2rem;
}
/*Humidity*/

.content-bar-humidity{
    width: 80%;
    margin-top: 2.5rem;
    margin-bottom: 2.5rem;
}

.posi-top-humidity{
    top: -80%;
}
.posi-bottom-humidity{
    bottom: -100%;
}.pos-percentagee{
    left: 80%;
}
/* .pos-0{

} */
.pos-50{
    left: 40%;
}
.pos-100{
    left: 70%;
}

/*Transitions*/
.component-fade-enter-active, .component-fade-leave-active {
    transition: opacity .3s ease;
}
.component-fade-enter, .component-fade-leave-to
/* .component-fade-leave-active below version 2.1.8 */ {
opacity: 0;
}
/*responsive*/
@media only screen and (max-width: 450px){/*Aplica de 0 a 450 lo que tenga dentro de este media query*/
    #app{
      height: 100%;
    }
    .container-principal{
        flex-direction: column;
    }
    .c-bar-search{
        width: 100vw;
        height: 100vh;
    }
    .cont-deegree {
        margin-top: 0.5rem;
        margin-bottom: 0rem;
    }
    .weather-state-bar {
        margin-top: 0.1rem;
        margin-bottom: 0rem;
    }
    /*Cards info*/
    .c-content-units{
        margin-right: 10%;
    }
    .c-card-w{
        width: 35%;
        margin-bottom: 1.5rem;
    }
    .c-content-weather{
        width: 100vw;
    }
    .card-info-today{
        flex-direction: column;
    }

}
</style>