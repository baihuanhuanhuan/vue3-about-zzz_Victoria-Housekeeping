<template>
    <div class="content">
    <footer class="footer" id="contact">
        <div class="logoo">
            <img src="/logo.png" alt="logo">
        </div>
        <div class="content-text">
            <a href="#" style="font-size: 15px;">隐私政策</a>
            <span style="font-weight: bold; color: white;">&nbsp;&nbsp;|&nbsp;&nbsp;</span>
            <a href="#" style="font-size: 15px;">自律公约</a>
            <span style="font-weight: bold; color: white;">&nbsp;&nbsp;|&nbsp;&nbsp;</span>
            <a href="#" style="font-size: 15px;">廉政举报</a>
            <span style="font-weight: bold; color: white;">&nbsp;&nbsp;|&nbsp;&nbsp;</span>
            <a href="#" style="font-size: 15px;">联系我们</a>
            <span style="font-weight: bold; color: white;">&nbsp;&nbsp;|&nbsp;&nbsp;</span>
            <a href="#" style="font-size: 15px;">加入我们</a>
            <p style="margin-top: 25px;">亲爱的市民朋友，新艾利都警方反诈劝阻电话"888-8888"系专门针对避免您财产被骗受损而设，请您一旦收到来带你，立即接听</p>
            <p>未成年成长关爱热线：877-8888（服务时间：8:00-23:00）</p>
            <p >© 2025 维多利亚家政服务. All rights reserved.  </p>
        </div>
    </footer>
    </div>
</template>

<script setup>

</script>

<style scoped>
.footer{
    /*padding:40px 20px;*/
    height: 30vh;
    display: flex;
    flex-direction: column;
    align-items:center;
    justify-content: center;
    position: relative;
    color: #888;
    /*background-color: rgba(255, 255, 255, 0.325);*/
    background-color: black;
    -webkit-touch-callout:none; /*系统默认菜单被禁用*/
    -webkit-user-select:none; /*webkit浏览器*/
    -khtml-user-select:none; /*早期浏览器*/
    -moz-user-select:none;/*火狐*/
    -ms-user-select:none; /*IE10*/
    user-select:none; 
}
.content{
    height: 20vh;
}
.content-text{
    padding-left: 100px;
    margin: 0;

}
.footer a{
    color: white;
    text-decoration: none;
    position:relative;
}
.footer a:hover{
    text-decoration:underline;
}
.footer p{
    margin: 0;
    font-size: 14px;
}

.logoo{
    /*width: 50px;
    height: 60px;*/
    position: absolute;
    left: 160px;
    display: flex;
    align-items: center;
}
.logoo img{
    width: 160px;
    height: auto;
}
</style>