<template>

    <div class="container">
        <div class="subheader-container">
            <h2 class="subheader-text text-right">Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s</h2>
        </div>

        <div class="services">
            <h1 class = "services-text text-left">Get Started</h1>
            <hr class ="line">
            <div class="row text-left">
                <div class="col">
                    <ul>
                        <li><h2>What am i eating?</h2></li>
                        <li><h2>What can i eat? (i'm pregnant, vegetarian, vegan) <span class="text-underline">(TBA)</span></h2></li>
                        <li><h2>Search for Recipes<span class="text-underline">(TBA)</span></h2></li>
                    </ul>
                </div>
            </div>
        </div>

        <section class="eating-card shadow mb-5 bg-white rounded">
            
            <h2 class = "text-center">What am i eating?</h2> 
            <div class="row text-center">
                <div class="col">
                     <!-- <button class = "btn" type = "submit">Randomize</button> -->
                    <input id = "txtName" type="text" class="search-field text-center" placeholder="Type your Food Item" v-model="searchQuery" v-on:keyup.enter="getQuery();">
                    <button class = "text-underline" v-on:click="getQuery(); ResultsisHidden = false">enter to look</button>
                        <!-- <a href="#" v-on:click="searchFood()">Lookup</a> -->
                </div>
            </div>
            <div class="row text-center">
                    <div class="col results" lazy> 
                    <!-- v-if="!ResultsisHidden" -->
                    <!-- <pre>{{data.hints[0].food}}</pre> -->
                        <h2>you searched for {{food.searched}},</h2>
                        <h3>Lets see... we found <span class="underline">'{{food.name}}'!</span> 
                        <div class="graph">
                        It's approximately {{food.calories}} calories, <br>
                        around {{food.protein}}g protein, <br>
                        contains about {{food.fat}}g of fat,<br>
                        and {{food.carbs}}g of carbs
                        </div>
                        </h3>            
                    </div>
            </div>
        </section>
    </div>
    
</template>



<script>

const axios = require('axios');
let app_id = process.env.VUE_APP_SECRET_APP_ID;
let app_key = process.env.VUE_APP_SECRET_APP_KEY;


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
            searchQuery:''
        }
    },
    methods:{
        getQuery:function(){
            //console.log(this.searchQuery);+this.searchQuery+
            axios
                .get('https://api.edamam.com/api/food-database/parser?nutrition-type=logging&ingr='+this.searchQuery+'&app_id='+app_id+'&app_key='+app_key)
                .then(response => {
                    this.food.searched = response.data.text,
                    this.food.name = response.data.parsed[0].food.label,
                    this.food.carbs = response.data.hints[0].food.nutrients.CHOCDF,
                    this.food.calories = response.data.hints[0].food.nutrients.ENERC_KCAL,
                    this.food.protein = response.data.hints[0].food.nutrients.PROCNT,
                    this.food.fat = response.data.hints[0].food.nutrients.FAT
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
    #txtName{
        padding:10px;
        margin:20px;
        border-radius:20px;
    }
    .line{
       width: 50%;
        margin: auto;
        margin-top: 5%;
        margin-bottom: 5%;
        transform: rotate(10deg);
        border-color: purple;
    }
    .eating-card{
        margin: 120px auto;
        padding:180px 0;
    }
</style>