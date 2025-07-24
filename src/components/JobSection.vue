<template>
    <section class="jobs" id="jobs" @mousemove="handleMouse" ref="aboutref" :class="{'inview-active': inview}">
        <div class="schoolin">
            <!--记得加网页链接-->
            <a href="https://jobs.mihoyo.com/#/campus" target="_blank">
            <div class="maintitle">校园招聘</div>
            <span class="subtitle">MORE INFORMATION</span>
            </a>
        </div>
        <div class="sociein">
            <a href="https://jobs.mihoyo.com/" target="_blank">
            <div class="maintitle">社会招聘</div>
            <span class="subtitle">MORE INFORMATION</span>
            </a>
        </div>
        <div class="vertical-img">
            <img src="/Joinus.png" alt="joinus">
        </div>
        <div class="XC-img" 
                :style="imgTransform1">
            <img src="/XC1.jpg" alt="XC1">
        </div>
        <div class="info-box1">
            <h2>核心信条</h2>
            <h3>您的心愿，我们的使命 (Our Creed: Your Wish is Our Mission)</h3>
            <div class="details1">
                <p>待维多利亚家政不仅是新艾利都家政行业的标杆，更是处理“特殊委托”的终极选择。我们追求的并非仅仅是完成任务，而是以无可挑剔的专业素养，为客户献上超越其想象的完美服务。在这里，您的每一次行动都将重新定义“可靠”的含义。加入我们，成为新艾利都最值得信赖的基石。</p>
            </div>
        </div>
        <div class="info-box2">
            <h2>团队理念</h2>
            <h3>优雅从容，追求卓越 (Our Philosophy: Elegance and Excellence)</h3>
            <div class="details1">
                <p>我们坚信，真正的专业素养体现在任何压力下的从容不迫与对细节的极致追求。维多利亚家政的每一位成员都是兼具优雅礼仪与强大实力的专家。我们营造的是一个简单纯粹、以实力和信赖为纽带的工作氛围，无论任务多么棘手，我们都将以最优雅的姿态将其解决。我们寻找的不是单纯的执行者，而是能与我们共同追求卓越的同行者。</p>
            </div>
        </div>
        <div class="info-box3">
            <h2>成长体系</h2>
            <h3>顶尖培训，应对万全 (Our Growth: Premier Training for Any Challenge)</h3>
            <div class="details1">
                <p>维多利亚家政为每一位成员提供业内最顶尖的成长路径与培训资源。从危机管理、情报分析到高风险目标处理，您将在这里接触到最前沿的实战技巧，与最优秀的团队一同成长。我们确保您拥有应对一切突发状况的能力，将您打造成能够独当一面的全能专家。</p>
            </div>
        </div>
        <div class="info-box4">
            <h2>薪酬礼遇</h2>
            <h3>丰厚回报，尊享生活 (Our Offer: Generous Rewards, Honored Living)</h3>
            <div class="details1">
                <p>我们深知您所创造的价值，并为此提供极具竞争力的回报与福利。在维多利亚家政，您的付出将得到最直接的肯定。除了丰厚的物质报酬，您还将获得新艾利都上层社会的社交资源与尊享礼遇，享受与您的能力相匹配的精英生活。我们不仅关心您的工作，更关心您的生活品质。</p>
            </div>
        </div>
        <div class="XC2-img" 
                :style="imgTransform2">
            <img src="/XC2.jpg" alt="XC2">
        </div>
    </section>
</template>

<script setup>
import{ref,onMounted,onUnmounted,computed,getCurrentInstance}from 'vue';
//响应式应用
const imgTransform1=ref({})
const imgTransform2=ref({})
//图片目标位置当前位置
const targetX1=ref(0), targetY1=ref(0);
const currentX1=ref(0), currentY1=ref(0);

const targetX2=ref(0), targetY2=ref(0);
const currentX2=ref(0), currentY2=ref(0);

//阻滞感
const damping =0.08;
let animationframeID=null;

    function handleMouse(e){
        const halfwindow=window.innerWidth/2;//一劈两半捏
        const normalizedY=(e.clientY/window.innerHeight-0.5)*-20;
        //鼠标判定
        if(e.clientX<halfwindow){
            targetX1.value=(e.clientX/halfwindow-0.5)*-20;
            targetY1.value=normalizedY;
            targetX2.value=0;
            targetY2.value=0;
        }
        else{
            targetX2.value=((e.clientX-halfwindow)/halfwindow-0.5)*-20;
            targetY2.value=normalizedY;
            targetX1.value=0;
            targetY1.value=0;
        }
    }
function animate(){
    //坐标差
    let dx1=targetX1.value-currentX1.value;
    let dy1=targetY1.value-currentY1.value;
    //当前位置向目标位置移动
    currentX1.value+=dx1*damping;
    currentY1.value+=dy1*damping;

    let dx2=targetX2.value-currentX2.value;
    let dy2=targetY2.value-currentY2.value;
    currentX2.value+=dx2*damping;
    currentY2.value+=dy2*damping;
    //更新transform
    imgTransform1.value={transform:`translate(${currentX1.value}px,${currentY1.value}px)`};
    imgTransform2.value={transform:`translate(${currentX2.value}px,${currentY2.value}px)`};
    animationframeID=requestAnimationFrame(animate);
}
const inview=ref(false);
const aboutref=ref(null);
let observer

onMounted(()=>{
    animate();
    observer=new IntersectionObserver(
        ([entry])=>{
                inview.value=entry.isIntersecting//直接赋值多次播放
        },{threshold:0.4}
    );
    /*   差分：
     ([entry])=>{
        if(entry.isIntersecting){
            inview.value=true;
        }
    }条件判断，当第一次进入该屏时entry.is....变为true同时inview.value=true
    但当离开可视区域时entry.is...变为false,if条件不满足,代码不执行也就不改变
    故动画只播放一次
    */
    if(aboutref.value){
        observer.observe(aboutref.value);
    }
});
onUnmounted(()=>{
    if(animationframeID){//停止循环防止泄露
        cancelAnimationFrame(animationframeID);
    }
    if(observer){
        observer.disconnect();
    }
})
</script>

<style>
    .jobs{
        height: 100vh;
        position: relative;
        overflow: hidden;
        -webkit-touch-callout:none; /*系统默认菜单被禁用*/
    -webkit-user-select:none; /*webkit浏览器*/
    -khtml-user-select:none; /*早期浏览器*/
    -moz-user-select:none;/*火狐*/
    -ms-user-select:none; /*IE10*/
    user-select:none; 
    }
    .schoolin{
        margin-top: 70px;
        margin-left: 43%;
        height: 300px;
        width: 70px;
        background-color: #dad39f;
        overflow: hidden;
        opacity: 0;
        transform: translateY(-100%);
        transition: all 0.8s ease-in;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .sociein{
        position: absolute;
        bottom: 0;
        margin-left: 50%;
        height: 300px;
        width: 70px;
        background-color: #dad39f;
        overflow: hidden;
        opacity: 0;
        transform: translateY(200%);
        transition: all 0.8s ease-in;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .jobs.inview-active .schoolin,
    .jobs.inview-active .sociein{
        opacity: 1;
        transform: translateY(0);
    }
    .schoolin a, .sociein a{
        text-decoration: none;
        position: relative;
        z-index: 2;
        color: white;
        font-size: 24px;
        display: flex;
        flex-direction: column;
        font-weight: bold;
        font-family: 'Microsoft Yahei',sans-serif;
        writing-mode: vertical-rl;/*竖向排版 */
        letter-spacing: 5px;/*竖排文字空隙*/
        transition: color 0.3s;
    }
    .schoolin::before, .sociein::before{
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgb(71,69,69);
        z-index: 1;
        transform: translateY(-100%);
        transition: transform 0.6s ease-out;
    }
    .schoolin:hover::before, .sociein:hover::before{
        transform: translateY(0);
    }
    .maintitle{
        color:rgb(255, 255, 255);
        font-size: 24px;
        font-weight: bold;
        font-family: 'Microsoft Yahei',sans-serif;
        writing-mode:vertical-rl;
        letter-spacing:8px;
        transition:color 0.3s;
    }
    .subtitle{
        color:rgb(252, 252, 252);
        font-size: 8px;
        letter-spacing: 1px;
        margin-top: 15px;
        opacity: 1;
        transform: translateY(0);
        transition: all 0.4s ease-out;
    }
    .schoolin:hover .subtitle, .sociein:hover .subtitle{
        transform: translateY(15px);
        color: rgb(255, 250, 152);
    }
    .schoolin:hover .maintitle, .sociein:hover .maintitle{
        color: rgb(255,250,152);
    }
    /*.schoolin a:hover, .sociein a:hover{
        color: #967a43;
    }
    .schoolin:hover, .sociein:hover{
        background-color: rgb(183,183,183) ;
        /*color:transparent;
        background-clip: text;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
    }*/

    /*文字&图片的滑入滑出*/
    .vertical-img{
        position: absolute;
        top:20px;
        right: 5%;
        width: 120px;
        height: 100%;
        overflow: hidden;
    }
    .vertical-img img{
        width: 100%;
        height: auto;
        opacity: 0;
        transform: translateY(-100%);
        transition:all 1s ease-out 0.2s;
    }
    .jobs.inview-active .vertical-img img{
        opacity: 1;
        transform: translateY(0);
    }
    .XC-img, .XC2-img{
        position: absolute;
        /*left: 5%;*/
        width: 400px;
        height: 100%;
        overflow: hidden;
    }
    .XC-img{
        top: 120px;
        left: 8%;
    }
    .XC2-img{
        top: 380px;
        right: 8%;
    }
    .XC-img img, .XC2-img img{
        width: 100%;
        height: auto;
        opacity: 0;
        /*transform: translateX(-100%);*/
        transition: all 0.6s ease-out;
    }
    .XC-img img{
        transform: translateX(-100%);
    }
    .XC2-img img{
        transform: translateX(200%);
    }
    .jobs.inview-active .XC-img img, .jobs.inview-active .XC2-img img{
        opacity: 1;
        transform: translateX(0);
    }
    .info-box1, .info-box2, .info-box3, .info-box4{
        position: absolute;
        /*top:380px;*/
        /*left: 8%;*/
        width: 485px;
        height: 95px;
        padding: 20px;
        box-sizing: border-box;/*防止padding撑开宽度*/

        /*玻璃拟态背景效果 */
        background: rgba(30, 30, 30, 0.14);
        backdrop-filter: blur(10px);
        -webkit-backdrop-filter: blur(10px);
        border: 1px solid rgba(255, 255, 255, 0.212);
        border-radius: 5px;

        color: black;
        overflow: hidden;
        transition: all 0.5s ease-out;
        /*transform-origin: left top;/*固定点 */
        /*transition: all 0.5s cubic-bezier(.3,1.2,.5,1);*/
    }
    .info-box1, .info-box2{
        left: 10%;
        transform-origin: left top;/*固定点 */
        transition: all 0.5s cubic-bezier(.3,1.2,.5,1);
    }
    .info-box1{
        top: 395px;
    }
    .info-box2{
        top: 530px;
    }
    .info-box3, .info-box4{
        right: 12%;
        transform-origin: right top;/*固定点 */
        transition: all 0.5s cubic-bezier(.3,1.2,.5,1);
    }
    .info-box3{
        top: 100px;
    }
    .info-box4{
        top: 235px;
    }
    .info-box1 h2, .info-box2 h2, .info-box3 h2, .info-box4 h2{
        margin: 0;
        padding: 0;
        font-size: 15px;
    }
    .info-box1 h3, .info-box2 h3, .info-box3 h3, .info-box4 h3{
        margin: 0;
        padding: 5px;
        font-size: 13px;
        font-weight: 400;
    }
    .info-box1 .details1, .info-box2 .details1, .info-box3 .details1, .info-box4 .details1{
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(145, 117, 71, 0.95);
        display: flex;
        flex-direction: column;
        justify-content: center;
        /*max-height: 0;
        opacity: 0;*/
        box-sizing: border-box;
        /*transform: translateX(-100%);*/
        transition: all 0.5s ease-in-out;
        /*padding-top: 0px;*/
        padding: 20px;
    }
    .info-box1 .details1, .info-box2 .details1{
        transform: translateX(-100%);
    }
    .info-box3 .details1, .info-box4 .details1{
        transform: translateX(200%);
    }
    .info-box1:hover .details1, .info-box2:hover .details1, .info-box3:hover .details1, .info-box4:hover .details1{
        transform: translateX(0);
        padding-top: 15px;
    }
    .info-box1:hover, .info-box2:hover, .info-box3:hover, .info-box4:hover{
        transform: scale(1.08);
        box-shadow: 0 8px 24px rgba(30,30,30,0.3);
    }
    .info-box1 .details1 p, .info-box2 .details1 p, .info-box3 .details1 p, .info-box4 .details1 p{
        margin: 10px 0 10px 0;
        font-size: 11px;
        line-height: 1.6;
        color: #ffffff;
    }
</style>