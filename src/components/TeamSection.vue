<template>
    <section class="team" id="team" @mousemove="handleMouse" ref="aboutref" :class="{'inview-active': inview}">
        <div class="text-container" style="textTransform">
            <h2 class="glow-gradient" v-html="textitems[0].title"></h2>
            <div class="title-group">
            <h3 v-html="textitems[0].title2"></h3>
            <p class="anno" v-html="textitems[0].annontation"></p>
            <p class="desc"  v-html="textitems[0].description1"></p>
            <br>
            <h5   v-html="textitems[0].title3"></h5>
            <p class="desc2" v-html="textitems[0].description2"></p>
            </div>
        </div>
        <div class="vertical-img">
            <img src="/Aboutus.png" alt="Aboutus">
        </div>
    </section>
</template>

<script setup>
import{ref,reactive,onMounted,onUnmounted,computed,getCurrentInstance}from'vue'
    const textitems=reactive([{
            title:'——走在新艾利都的家政行业前沿&nbsp&nbsp&nbsp&nbsp<br>&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp&nbsp您的心愿就是我们的使命——',
            title2:'为您展现的',
            annontation:'ABOUT VICTORIA HOUSEKEEPING',
            description1:'维多利亚家政是新艾利都声名显赫的家政服务品牌，致力于为高端客户提供无可挑剔的、超出想象的至臻服务。维多利亚家政的业务范围不仅涵盖顶级的日常家务与生活管理，更能完美处理客户的各类“特殊委托”，并围绕其核心业务打造了安保、咨询及危机处理等多元化服务。<br><br>秉承着“您的心愿就是我们的使命”这一服务信条，维多利亚家政始终走在“特殊业务处理”领域的最前沿，在危机应对、高危目标处理、空洞灾害防护等领域积累了旁人难以企及的实战经验与处理能力。<br><br>维多利亚家政总部位于新艾利都的中央商务区，其服务网络与影响力遍及城中各大关键区域。目前，公司拥有业内最顶级的精英团队，每一位成员都经过严苛选拔，是兼具优雅礼仪与强大实力的专业人士，随时准备为客户提供最可靠的解决方案。<br>',
            title3:'维多利亚家政的服务理念',
            description2:'Perfect &nbsp Service &nbsp|&nbsp Absolute &nbsp Discretion &nbsp|&nbsp Ultimate &nbsp Solution'
        }])
    const textTransform=ref({})
    function handleMouse(e){
        const x=(e.clientX/window.innerWidth-0.5)*-20
        const y=(e.clientY/window.innerHeight-0.5)*-20
        textTransform.value={
            transform:`translate(${x}px,${y}px)`
        }
    }
    const inview=ref(false)
    const aboutref=ref(null)
    let observer
    onMounted(()=>{
        observer=new IntersectionObserver(
            ([entry])=>{
                inview.value=entry.isIntersecting
            },{threshold:0.4}
        )
        observer.observe(aboutref.value)
    })
    onUnmounted(()=>{
        observer.disconnect()
    })
</script>

<style scoped>
    /*控制内部所有文字的容器兼动画状态 */
    .team{
        position: relative;
        overflow: hidden;
        -webkit-touch-callout:none; /*系统默认菜单被禁用*/
    -webkit-user-select:none; /*webkit浏览器*/
    -khtml-user-select:none; /*早期浏览器*/
    -moz-user-select:none;/*火狐*/
    -ms-user-select:none; /*IE10*/
    user-select:none; 
    }
    .text-container{
        opacity: 0;
        transform: translateY(100px);
        transition: all 0.8s cubic-bezier(.3,1.2,.5,1);
    }
    /*inview-active被加上时的目标状态 */
    .team.inview-active .text-container{
        opacity: 1;
        transform: translateY(0);
    }
    .vertical-img{
        position: absolute;
        top:10px;
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
        transition: all 1s ease-out 0.2s;
    }
    .team.inview-active .vertical-img img{
        opacity: 1;
        transform: translateY(0);
    }
    .title-group{
        text-align: center;
    }
    .title-group h3{
        margin-bottom: -3px;
    }
    .anno{
        color:#b8b8b8;
        font-size: 10px;
        letter-spacing: 2px;
        margin-top: 0;
    }
    .desc{
        margin: 0 320px;
        font-size: 14px;
        font-family:'Courier New', Courier, monospace;
    }
    .desc2{
        margin-top: 0;
        font-size: 12px;
    }
    h5{
        margin-bottom: 8px;
    }
    h2{
        font-family: 'Microsoft Yahei',sans-serif;
        font-weight: 101;
        font-size: 33px;
        text-align: center;
        padding-top: 13vh;
        line-height: 1.6;
    }
    .glow-gradient{
        background: linear-gradient(90deg,#dad39f,#b6af88 20%, #6c665c 40%, #231d2c 60%, #474144 80%, #cbc59c);
        background-size: 200% auto;
        color:transparent;
        background-clip: text;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        animation: shine 4s linear infinite;
        letter-spacing: 2px;
    }
    @keyframes shine{
        to{
            background-position: -200% center;
        }
    }
</style>