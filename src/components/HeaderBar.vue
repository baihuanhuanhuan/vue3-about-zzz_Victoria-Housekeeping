<template>
    <header id="mainheader">
        <!--这里记得放logo-->
        <div class="logo">
            <img src="/logo.png" alt="公司logo" width="60px" height="60px">
            <span class="company_name">维多利亚家政</span>
        </div>
        <!--这里是细则-->
        <!--用@click.prevent阻止a标签默认跳转的行为然后带一个发射信号函数-->
        <nav class="nav-links">
            <a href="#" @click.prevent="emitNavigate(0)">首页</a>
            <a href="#" @click.prevent="emitNavigate(1)">团队成员</a>
            <a href="#" @click.prevent="emitNavigate(2)">关于我们</a>
            <a href="#" @click.prevent="emitNavigate(3)">加入我们</a>
        </nav>
    </header>
</template>

<script setup>
    import { defineEmits } from 'vue';
    //发出的信号
    const emit=defineEmits(['navigate']);
    function emitNavigate(screenIndex){
        emit('navigate',screenIndex);
    }
    window.addEventListener('scroll',function(){
    const header=this.document.getElementById("mainheader");
    if(window.scrollY>50){
        header.classList.add('active');
    }else{
        header.classList.remove('active');
    }
});
</script>

<style>
    header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: rgba(255, 255, 255, 0);
    padding: 5px 20px;
    position: fixed;
    top: 0;
    width: 100%;
    transition: background-color 0.5s ease;
    z-index: 1000;
}
.left{
    display: flex;
    align-items: center;
}
.company_name{
    margin-left: 10px;
    font-size: 20px;
    font-weight: bold;
    /*justify-content: center;*/
    color: rgb(37, 30, 46);
    -webkit-touch-callout:none; /*系统默认菜单被禁用*/
    -webkit-user-select:none; /*webkit浏览器*/
    -khtml-user-select:none; /*早期浏览器*/
    -moz-user-select:none;/*火狐*/
    -ms-user-select:none; /*IE10*/
    user-select:none; 
}
.nav-links{
    /*margin: 60px;*/
    text-decoration: none;
    font-size: 10px;
    gap: 25px;
    margin-right: 100px;
    /*box-shadow:#a4a4a4;*/
    /*margin-bottom: 20px;*/
    -webkit-touch-callout:none; /*系统默认菜单被禁用*/
    -webkit-user-select:none; /*webkit浏览器*/
    -khtml-user-select:none; /*早期浏览器*/
    -moz-user-select:none;/*火狐*/
    -ms-user-select:none; /*IE10*/
    user-select:none; 
}

.nav-links a{
    text-decoration: none;
    margin-left: 20px;
    color: rgb(56, 56, 56);
    font-size: 12px;
    transition: color 0.3s ease;
}

.nav-links a:hover{
    color: #c19552;
}

header.active{
    background-color: #d0d0d0;
}

.logo{
    display: flex;
    align-items: center;
}
</style>