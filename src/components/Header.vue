<template>
<div>
    <nav id="myNav" class="navbar navbar-expand-lg navbar-dark fixed-top bg-dark">
        <img class="logo" v-bind:src = "require('../assets/animat-search-color.png')" alt="">   
        <h3 class = "logo-title">food_knowledge</h3>
        <div id="navbarNavDropdown" class="navbar-collapse collapse">
            <ul class="navbar-nav mr-auto">
            </ul>
            <ul class="navbar-nav">

                <!-- <li class="nav-item menu-item">
                    <a class="nav-link" href="#">Our Services</a>
                </li>
                <li class="nav-item menu-item">
                    <a class="nav-link" href="#">Portfolio</a>
                </li>
                <li class="nav-item menu-item">
                    <a class="nav-link" href="#">About Us</a>
                </li>
                <li class="nav-item menu-item">
                    <a class="nav-link" href="#">Blog</a>
                </li>
                <li class="nav-item menu-item">
                    <a class="nav-link" href="#">Contact</a>
                </li> -->
                
            </ul>
        </div>
    </nav>
</div>
</template>


<script>
  
export default {
    name:'Header'
}
</script>

<style scoped>
    .navbar{
        background-color:rgba(255,255,255,1)!important;
    }
    .logo{
        width:40px;
    }
    .logo-title{
        margin:0;
    }
    li.menu-item{
        padding:10px;
        font-size:14px;
        color:white;
    }
</style>

