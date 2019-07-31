<template>

    <div class="container">
        <div class="subheader-container">
            <h2 class="subheader-text text-right">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s</h2>
        </div>

        <div class="services">
            <h1 class = "services-text text-left" data-aos="fade-right">Get Started</h1>
            <hr class ="line">
            <div class="row text-left">
                <div class="col">
                    <ul>
                        <li data-aos="fade-right" data-aos-duration="1000"><h2>What am i eating?</h2></li>
                        <li data-aos="fade-right" data-aos-duration="1200"><h2>What can i eat? (i'm pregnant, vegetarian, vegan) <span class="text-underline">(TBA)</span></h2></li>
                        <li data-aos="fade-right" data-aos-duration="1700"><h2>Search for Recipes <span class="text-underline">(TBA)</span></h2></li>
                    </ul>
                </div>
            </div>
        </div>

        <section class="eating-card shadow-lg mb-5 bg-white rounded" data-aos="fade-up">
            <h2 class = "text-center">What am i eating?</h2> 
            <div class="row text-center">
                <div class="col">
                     <!-- <button class = "btn" type = "submit">Randomize</button> -->
                    <input id = "txtName" type="text" class="search-field text-center" placeholder="Search.." v-model="searchQuery" v-on:keyup.enter="getQuery(); ResultsisHidden = false">
                    <button class = "text-underline" v-on:click="getQuery(); ResultsisHidden = false">database lookup</button>
                </div>
            </div>
            <div class="row text-center">
                    <div class="col results" lazy v-if="!ResultsisHidden"> 
                    <!-- v-if="!ResultsisHidden" -->

                        <h2>you searched for {{food.searched}},</h2>
                        <h3>And... we found <span class="underline" data-aos="fade-in">'{{food.name | capitalize}}'!</span> 
                            <div class="nutrition"  data-aos="fade-up" data-aos-anchor-placement="top-center" data-aos-duration="1200">
                                <h2 class = "sidebar-title text-underline" data-aos="fade-right" data-aos-duration="1500">Nutrition</h2>
                                It's approximately <span class="text-underline text-lg">{{food.calories}}</span> calories(kcal), <br>
                                around <span class="text-underline text-lg">{{food.protein}} g</span> of protein, <br>
                                contains about <span class="text-underline text-lg">{{food.carbs}} g</span> of carbs,<br>
                                and <span class="text-underline text-lg">{{food.fat}} g</span> of fat.
                               
                            </div>
                            <div class="average-intake"  data-aos="fade-up" data-aos-anchor-placement="top-center" data-aos-duration="1200">
                                <h2 class = "sidebar-title text-underline" data-aos="fade-right" data-aos-duration="1200">Average</h2>
                               {{food.name | capitalize}} would only take <span class="text-underline text-lg">{{avgIntake.avgCalories}}</span>
                                of your daily 2000 kcal diet,
                                <br>
                                <span class="text-underline text-lg">{{avgIntake.avgProtein}}</span> of your daily intake of 50g protein,<br>
                                <span class="text-underline text-lg">{{avgIntake.avgCarbs}}</span> of your daily intake of 275g carbs,<br>
                                <span class="text-underline text-lg">{{avgIntake.avgFat}}</span> of your daily intake of 60g fat.
                                                            
                            </div>
                        </h3>            
                    </div>
            </div>
        </section>
    </div>
</template>

<script>
import AOS from 'aos'
import 'aos/dist/aos.css';

const axios = require('axios');
let app_id = process.env.VUE_APP_SECRET_APP_ID;
let app_key = process.env.VUE_APP_SECRET_APP_KEY;

AOS.init();

export default {
    name:'Body',
    data:function(){
        return{
            ResultsisHidden: true,
            errorMsg:'Nothing Found, Try Again',
            food: {
                searched:'',
                name:'',
                carbs:'',
                calories:'',
                protein:'',
                fat:''
            },
            avgIntake:{
                avgCarbs:'',
                avgCalories:'',
                avgFat:'',
                avgProtein:'',
            },
            searchQuery:''
        }
    },
    filters:{
        capitalize: function(word){
           if (!word) return ''
            word = word.toString()
            return word.charAt(0).toUpperCase() + word.slice(1)
        }
    },
    methods:{
        getQuery:function(){
            let dailyCarbs = 275
            let dailyCalories = 2000
            let dailyFat = 60
            let dailyProtein = 50
            //console.log(this.searchQuery);+this.searchQuery+
            axios
                .get('https://api.edamam.com/api/food-database/parser?nutrition-type=logging&ingr='+this.searchQuery+'&app_id='+app_id+'&app_key='+app_key)
                .then(response => {
                    this.food.searched = response.data.text,
                    this.food.name = response.data.parsed[0].food.label,
                    this.food.carbs = response.data.hints[0].food.nutrients.CHOCDF.toFixed(2),
                    this.food.calories = response.data.hints[0].food.nutrients.ENERC_KCAL.toFixed(1),
                    this.food.protein = response.data.hints[0].food.nutrients.PROCNT.toFixed(2),
                    this.food.fat = response.data.hints[0].food.nutrients.FAT.toFixed(2),

                    this.avgIntake.avgCarbs = ((response.data.hints[0].food.nutrients.CHOCDF/dailyCarbs)*100).toFixed(1) + '%',
                    this.avgIntake.avgCalories = ((response.data.hints[0].food.nutrients.ENERC_KCAL/dailyCalories)*100).toFixed(2) + '%',
                    this.avgIntake.avgProtein = ((response.data.hints[0].food.nutrients.PROCNT/dailyProtein)*100).toFixed(1) + '%',
                    this.avgIntake.avgFat = ((response.data.hints[0].food.nutrients.FAT/dailyFat)*100).toFixed(1) + '%'
                    // console.log(this.avgCarbs);
                })
                .catch(function(error){
                   console.log(error);
            })
        }
    },
    mounted(){
        // this.data=null;
    }
}
</script>

<style scoped>
    .subheader-container{
        margin:80px 0 150px auto;
        width:60%;
    }
    .subheader-text{
        line-height:1.5;
    }
    .col>h3{
        text-align:center;
    }
    .text-underline{
        border: tomato;
        border-style: none none solid;
        border-width: 10px 0px 10px;
        line-height:1;
        width:fit-content;
        transition:0.3s ease;
    }
    .text-underline:hover{
         border-width: 0px 0px 5px;
    }
    .text-lg{
        font-size:120%;
        font-weight:bold;
    }
    #txtName{
        padding: 5px;
        margin: 35px 20px;
        border-radius: 5px;
        width: 201px;
    }
    .line{
        width: 52%;
        -webkit-transform: rotate(45deg);
        transform: rotate(0deg);
        border-color: tomato;
        border-width: 10px;
        margin-top: -15px;
        position: relative;
        left: -50%;
    }
    .eating-card{
        margin: 120px auto;
        padding:120px 0;
    }
    .nutrition,.average-intake{
        line-height:2.8;
        margin-top:50px;
    }
    .sidebar-title{
        position:absolute;
        font-size:35px;
        margin-top:90px;
        left:-40px;

    }
</style>