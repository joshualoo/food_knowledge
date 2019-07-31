<template>
    <div class="">
        <div class="hero-container shadow-lg bg-white rounded">
            <div class="hero-img"></div>

                <div class="shape-right"></div>
                <div class="shape-left"></div>

            <div class="header-container ">
                <h1>Learn about Food</h1>
                <h2 class = "text-white">Feeling Adventurous? / Just curious?</h2>
            <button class="cta"> <span class="hightlight">Let's go!</span></button>
            </div>
        </div>

    </div>
</template>

<script>

export default {
    name:'Hero'
}
</script>

<style scoped>
    .hero-container{
        height:100vmin;
        white-space:nowrap;
    }
    .hero-img{
        background:url('../assets/bg-2.jpg');
        background-attachment: fixed;
        width:100%;
        height:100%;
        filter:brightness(0.7);
        background-size:cover;
        background-position-y: 100px;
    }
    .header-container>h1,.sec-header-container>h3{
        color:rgba(255,255,255,0.99);
    }
    .shape-left,.shape-right{
        position:absolute;
        width:40%;
        height:600px;
        filter:opacity(0.15);
        background: #E0EAFC;  /* fallback for old browsers */
        background: -webkit-linear-gradient(to right, #CFDEF3, #E0EAFC);  /* Chrome 10-25, Safari 5.1-6 */
        background: linear-gradient(to right, #CFDEF3, #E0EAFC); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
        animation-duration:2s;
    }
    .shape-right{
        right: -66px;
        top: 10%;
        clip-path: polygon(68% 0, 0 83%, 100% 100%);
    }
    .shape-left{
        width:40%;
        left:-100px;
        top:40%;
        clip-path: polygon(60% 0, 0 80%, 100% 100%);
    }
    .header-container,.sec-header-container{
        text-align:center;
        position:absolute;
        top:35%;
        left:50%;
        transform:translateX(-50%);
    }

</style>
