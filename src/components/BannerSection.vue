<template>
<section class="banner">
        <div class="banner-overlay">
            <h1>欢迎访问维多利亚家政</h1>
            <p>Your wishes are our mission.</p><!--这个记得要单独做一个漂亮的艺术字啪地放上去-->
        </div>
</section>
</template>

<script setup>

</script>

<style scoped>
.banner{
    height: 100vh;
    width: 100vw;
    background: linear-gradient(rgba(255,255,255,0.4),rgba(255,255,255,0.4)),
            url("/banner.png") center no-repeat;
    background-size: cover;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    position: relative;
    /*overflow: hidden;*/
}
.banner-overlay{
    color:white;
    animation: fadeIn 2s ease forwards;
}
.banner-overlay h1{
    font-size:50px;
    margin-bottom: 20px;
    text-shadow: 2px 2px 5px rgba(0,0,0,0.5);
}

.banner-overlay p{
    font-size: 30px;
    opacity: 0.8;
    text-shadow: 2px 2px 5px rgba(0,0,0,0.5);
}
/*淡出一下*/
@keyframes fadeIn{
    0%{
        opacity: 0;
        transform:translateY(20px);
    }
    100%{
        opacity: 1;
        transform:translateY(0);
    }
}
</style>