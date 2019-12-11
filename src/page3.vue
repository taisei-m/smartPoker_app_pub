<template>
<v-ons-page>
     <div class="gradation" style="padding-top:5%;">
    <g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#eeeeee"><path d="M143.19336,21.43001c-0.26705,0.00844 -0.53341,0.03181 -0.79785,0.06999h-34.89551c-2.58456,-0.03655 -4.98858,1.32136 -6.29153,3.55376c-1.30295,2.2324 -1.30295,4.99342 0,7.22582c1.30295,2.2324 3.70697,3.59031 6.29153,3.55376h18.53256l-66.59961,66.59961c-1.8722,1.79752 -2.62637,4.46674 -1.97164,6.97823c0.65473,2.51149 2.61604,4.4728 5.12753,5.12753c2.51149,0.65473 5.18071,-0.09944 6.97823,-1.97165l66.59961,-66.59961v18.53255c-0.03655,2.58456 1.32136,4.98858 3.55376,6.29153c2.2324,1.30295 4.99342,1.30295 7.22582,0c2.2324,-1.30295 3.59031,-3.70697 3.55376,-6.29153v-34.9235c0.28889,-2.08845 -0.35639,-4.19816 -1.76411,-5.76769c-1.40772,-1.56953 -3.43507,-2.43964 -5.54253,-2.3788zM35.83333,21.5c-7.83362,0 -14.33333,6.49972 -14.33333,14.33333v100.33333c0,7.83362 6.49972,14.33333 14.33333,14.33333h100.33333c7.83362,0 14.33333,-6.49972 14.33333,-14.33333v-43c0.03655,-2.58456 -1.32136,-4.98858 -3.55376,-6.29153c-2.2324,-1.30295 -4.99342,-1.30295 -7.22582,0c-2.2324,1.30295 -3.59031,3.70697 -3.55376,6.29153v43h-100.33333v-100.33333h43c2.58456,0.03655 4.98858,-1.32136 6.29153,-3.55376c1.30295,-2.2324 1.30295,-4.99342 0,-7.22582c-1.30295,-2.2324 -3.70697,-3.59031 -6.29153,-3.55376z"></path></g></g>
<v-ons-card>
  <div>

    <h1 class="box17" >WINNER:{{ranking[0].name}}</h1>

    <ul v-for ="(item,index) of ranking" v-bind:key="index" class="ranking">
      <ol>{{index+1}}位:{{item.name}}</ol>
    </ul>
  </div>
  </v-ons-card>
  <div>
   <a @click="submit()" class="btn">
    もう一度
  </a>
  </div>
     </div>
  </v-ons-page>
</template>

<script>
import page1 from './page1.vue'
import page2 from './page2.vue'

export default {
  data() {
    return {
      ranking: this.$store.state.ranking,
    };
  },
  created() {
  },
  methods: {
    submit: function(){
    this.$store.commit("navigator/push", page1);
  }
  }
};
</script>

<style scoped>
.gradation{
    margin-top: -60px;
    width: 100%;
    height: 100%;
    font-family: "Exo", sans-serif;
    color: black;
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: gradientBG 15s ease infinite;

}


@keyframes gradientBG {
    0% {
        background-position: 0% 50%;
    }
    50% {
        background-position: 100% 50%;
    }
    100% {
        background-position: 0% 50%;
    }
}
h1{
  text-align: center;
}

body{
  margin: 0;
  padding: 0;
  background: #05151a;
}

.neon{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  margin: 0;
  padding: 0 20px;
  font-size: 3em;
  color: #ffd700;
  text-shadow: 0 0 50px #ffd700;
  letter-spacing: 5px;
}

.neon:after{
  content: attr(data-text);
  position: absolute;
  top: 0;
  left: 0;
  padding: 0 20px;
  z-index: -1;
  color: #ffd700;
  filter: blur(15px);
}

.neon:before{
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #ffd700;
  z-index: -2;
  opacity: .3;
  filter: blur(50px);
}
.ranking{
text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
}
.ranking ol{
    position: relative;
    margin: 0;
    padding: 0 0 0 16px;
    border-bottom: 1px dotted #ccc;
}
.ranking ol::before{
    position: absolute;
    top: 7px;
    left: 1px;
    color: #d05;
    content: "★";
    font-size: 9px;
}
.ranking ol:first-child::before,
.ranking ol:nth-child(2)::before,
.ranking ol:nth-child(3)::before{
    position: absolute;
    top: 1px;
    left: 0;
    width: 0;
    height: 0;
    border: 6px solid transparent;
    border-bottom: 10px solid #fb0;
    content: "";
}
.ranking ol:first-child::after,
.ranking ol:nth-child(2)::after,
.ranking ol:nth-child(3)::after{
    position: absolute;
    top: 9px;
    left: 0;
    width: 0;
    height: 0;
    border: 6px solid #fb0;
    border-top: 3px solid transparent;
    border-bottom: 6px solid #f90;
    content: "";
}
.ranking ol:nth-child(2)::before{
    border-bottom: 10px solid #ccc;
}
.ranking ol:nth-child(2)::after{
    border: 6px solid #ccc;
    border-top: 3px solid transparent;
    border-bottom: 6px solid #aaa;
}
.ranking ol:nth-child(3)::before{
    border-bottom: 10px solid #d98;
}
.ranking ol:nth-child(3)::after{
    border: 6px solid #d98;
    border-top: 3px solid transparent;
    border-bottom: 6px solid #c76;
}
.ranking ol span{
    color: #9ab;
    font-size: 11px;
}

.box17{
    margin:2em 0;
    position: relative;
    padding: 0.5em 1.5em;
    border-top: solid 2px black;
    border-bottom: solid 2px black;
    color: rgba(0,0,0,0.6);
    text-shadow: 2px 8px 6px rgba(0,0,0,0.2),
               0px -5px 16px rgba(255,255,255,0.3);
}
.box17:before, .box17:after{
    content: '';
    position: absolute;
    top: -10px;
    width: 2px;
    height: -webkit-calc(100% + 20px);
    height: calc(100% + 20px);
    background-color: black;
}
.box17:before {left: 10px;}
.box17:after {right: 10px;}
.box17 p {
    margin: 0;
    padding: 0;
}

.wrapper {
  margin: 150px auto;
  text-align: center;
  width: 100%;
  position: relative;
}
.btn{
  padding: 15px 100px;
  margin:10px 4px;
  color: #fff;
  font-family: sans-serif;
  text-transform: uppercase;
  text-align: center;
  position: relative;
  text-decoration: none;
  /* display:inline-block; */
  /* display: flex; */
  /* justify-content: center; */
  /* align-items: center; */
}
.btn::before {
  content: '';
  position: absolute;
  bottom: 0%;
  left: 0px;
  width: 100%;
  height: 1px;
  background: #6098FF;
  display: block;
  -webkit-transform-origin: right top;
  -ms-transform-origin: right top;
  transform-origin: right top;
  -webkit-transform: scale(0, 1);
  -ms-transform: scale(0, 1);
  transform: scale(0, 1);
  -webkit-transition: transform 0.4s cubic-bezier(1, 0, 0, 1);
  transition: transform 0.4s cubic-bezier(1, 0, 0, 1)
}

.btn:hover::before {
  -webkit-transform-origin: left top;
  -ms-transform-origin: left top;
  transform-origin: left top;
  -webkit-transform: scale(1, 1);
  -ms-transform: scale(1, 1);
  transform: scale(1, 1)
}

</style>

