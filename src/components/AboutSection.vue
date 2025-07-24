<template>
    <!---->
    <section class="about" id="about" @mousemove="handleMouse" :class="{'enter':inView}" ref="aboutRef">
        <div class="about-container">
            <!--图片区域（动画）-->
            <!--<Transition
                 name="img-slide"
                 mode="out-in">-->
                <div class="image" 
                     :style="imageTransform">
                    <img :src="ImgItem.image" :alt="ImgItem.title" width="380"/>
                </div>
            <!--</Transition>-->
            <!--这里是文字动画区域-->
            <!--<Transition
                  name="text-slide"
                  mode="out-in" > -->
                <div class="text">
                    <h1>{{ ImgItem.title }}</h1>
                    <p v-html="ImgItem.description"></p>
                    <!--图标选择器新址-->
                    <div class="selector">
                        <img
                          v-for="(item, i) in items"
                          :key="i"
                          :src="item.icon"
                          :class="{ active: i === index }"
                          @click="selectItem(i)"
                          :alt="item.title"
                        />
                    </div>
                </div>
            <!--</Transition>-->
                <!--小图标切换-->
                <!--<div class="selector">
                    <img
                        v-for="(item,i) in items" 
                        :key="i" 
                        :src="item.icon" 
                        :class="{active:i===index}"
                        @click="selectItem(i)"
                        alt="切换按钮"
                        />
                </div>-->
            </div>
        <!--图标选择器旧址二号-->
        <div class="vertical">
            <img src="/Teammembers.png" alt="Teammembers">
        </div>
    </section>
</template>

<script setup>
    import{ref,reactive,onMounted,onUnmounted,computed, getCurrentInstance}from'vue'
    //当前选中项下标
    const index=ref(0)
    const items=reactive([{
        image:'/LKN.png',
        icon:'/LKN_icon.png',
        title:'冯·莱卡恩',
        description:'不管什么事情都能妥善解决，是顾客最信赖的执事，是团队最坚实的后盾。<br>理性又明智，优雅如绅士，容不得一点污渍。<br>理性又明智，优雅如绅士，容不得一点污渍。<br>认定自己跟随的人之后，会向其献上绝对的忠诚。<br>虽然表面上优雅理性，但面对某些危险时会流露出与生俱来的野性。'
    },
    {
        image:'/LN.png',
        icon:'/LN_icon.png',
        title:'亚历山德丽娜·莎芭丝缇安',
        description:'<strong>「仲夏夜之梦舞曲」</strong><br>精致柔和的曼妙旋律，在丽娜身上自然而然地流淌。<br><strong>「命运交织协奏曲」</strong><br>玩偶们演绎的附加乐章，最好竖起所有耳朵听。<br><strong>「新新世界交响曲」</strong><br>激昂有力却不失优雅，揍人也是一如既往地美丽。<br><strong>「沉默悲怆奏鸣曲」</strong><br>看到丽娜走进厨房时，很多人脑中会响起的配乐'
    },
    {
        image:'/AL.png',
        icon:'/AL_icon.png',
        title:'艾莲·乔',
        description:'三言两语，简单一点<br>麻烦的事情在这里可行不通，一切从简。<br>劳逸结合，轻松一点<br>适时休息，当然是为了工作... 的时候少点心烦。<br>全神贯注，小心一点<br>怕她不认真，也怕她过于认真，好在受苦的是敌人。<br>剥开糖纸，甜蜜一点<br>把棒棒糖叼在嘴里，把少女的心思藏在怀里。'
    },
    {
        image:'/KL.png',
        icon:'/KL_icon.png',
        title:'可琳·威克斯',
        description:'无论是不是家政工作，只要交给她就没问题！<br><span class="small-text">（唉、唉唉？可、可琳并没有这么厉害！）</span><br>乖巧听话、认真负责，不惧任何脏活与累活！<br><span class="small-text">（请、请等一下！可琳并不是这样的！）</span><br>永不会让合作者受拖累，任何事接手就会负责到底！<br><span class="small-text">（拜托了，请好好听可琳说话！这些夸大的宣传会让顾客误会的！）</span><br>可琳，她是可以在新艾利都上找到的最好的女仆！<br><span class="small-text">（呜呜，请、请不要把这份报道发出去！这不是真正的可琳！）</span>'
    }])
    //计算当前展示内容
    const ImgItem=computed(()=>items[index.value])
    //切换选中项目
    function selectItem(i){
        index.value=i;
    }
    //视差动效
    const imageTransform=ref({})
    function handleMouse(e){
        const x=(e.clientX/window.innerWidth-0.5)*-50
        //const y=(e.clientY/window.innerHeight-0.5)*-30
        imageTransform.value={
            transform:`translate(${x}px)`
        }
    }
    //视口进入/离开检测，切换出入场动画
    const inView=ref(false)
    const aboutRef=ref(null)//观察元素位置
    let observer//保存实例
    onMounted(()=>{
        observer=new IntersectionObserver(
            ([entry])=>{
                inView.value=entry.isIntersecting
        },{threshold:0.4}
        )
        observer.observe(aboutRef.value)
    })
    onUnmounted(()=>{
        observer.disconnect()
    })
    
</script>

<style>
/*整个的 */
.about{
    height: 100vh;
    display: flex;
    align-items: center;/*垂直居中 */
    position: relative;
    justify-content: center;
    overflow: hidden;
    /*background-color: rgba(255, 242, 220, 0.7);*/
}
.about-container{
    margin-bottom: 30px;
    margin-left: -100px;
    width: 100%;
    padding: 0 100px;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    /*background: rgba(240,240,240,0.7);*/
    border-radius: 32px;
    /*box-shadow: 0 8px 24px rgba(0,0,0,0.1);*/
    opacity: 1;
    flex-grow: 1;/**新增2 */
    -webkit-touch-callout:none; /*系统默认菜单被禁用*/
    -webkit-user-select:none; /*webkit浏览器*/
    -khtml-user-select:none; /*早期浏览器*/
    -moz-user-select:none;/*火狐*/
    -ms-user-select:none; /*IE10*/
    user-select:none; 
}
.about.enter .text,
.about.enter .image,
.about.enter .vertical img
{
    opacity: 1;
    transform: translateX(0);
}
.vertical{
    position: absolute;
    right: 5%;
    top:15px;
    width: 120px;
    height: 100%;
    overflow: hidden;/*隐藏溢出 */
}
.vertical img{
    width: 100%;
    height: auto;
    opacity: 0;
    transform: translateY(-100%);
    transition: all 1s ease-out 0.2s;
}
.about.enter .vertical img{
    transform: translateY(0);/**归位 */
}
.image{
    flex: 1.2;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: transform 0.3s;/**捧油，这里是切入动画啊 */
    transform: translateX(-300px);
    opacity: 0;
    margin-left: 4%;
    transition: all 0.8s cubic-bezier(.3,1.2,.5,1);
}
.image img{
    width: 700px;
    height: auto;
    /*box-shadow: 0 4px 16px rgba(64,64,64,0.1);*/
}
.text{
    writing-mode: horizontal-tb;
    margin-right: 6%;
    flex:1;
    padding: 0 30px;
    text-align: left;
    transform: translateX(100px);
    opacity: 0;
    transition: all 0.8s ease 0.2s;
}
.text h1{
    writing-mode: horizontal-tb;
    font-size: 36px;
    margin-bottom: 24px;
    color:black
}
.text p{
    font-size: 18px;
    color:#666;
}
/**小图标 */
.selector{
    position:absolute;
    width: 100%;
    left: 50%;
    padding-bottom: 32px;
    transform: translateX(-50%);/*水平居中 */
    display: flex;
    justify-content: center;
    gap : 20px;
    /*z-index: 999;*/
    margin-top: 30px;
    margin-bottom: 18px;
}
.selector img{
    width: 48px;
    cursor: pointer;
    opacity: 0.55;
    transition: opacity 0.3s,transform 0.3s;
}
.selector img.active{
    opacity: 1;
    transform: scale(1.18);
}
/**图片切换动画 */
/*
.img-slide-enter-active{
    transition: all 0.8s ease-out;
}*/
/*
.img-slide-leave-active{
    transition: all 0.8s ease-out;
    position: absolute;
}*/
/**
@keyframes img-in{
    0% {opacity: 0; transform: translateX(200px);}
    100% {opacity: 1; transform: translateX(0);}
}
@keyframes img-out{
    0% {opacity: 1; transform: translateX(0px);}
    100% {opacity: 0; transform: translateX(-200);}
}*/
 /*
.img-slide-leave-to{
    transform: translateX(-200px);
    opacity: 0;
}
 
.img-slide-enter-from{
    transform: translateX(200px);
    opacity: 0;
}

/**切文字 
.text-slide-enter-active{
    transition: all 0.8s ease-out;
    /*position: absolute;
}
.text-slide-leave-active{
    transition: all 0.8s ease-out;
}*/
/** 
@keyframes text-in{
    0% {opacity: 0; transform: translateX(-200px);}
    100% {opacity: 1; transform: translateX(0);}
}
@keyframes text-out{
    0% {opacity: 1; transform: translateX(0px);}
    100% {opacity: 0; transform: translateX(200);}
}
*/
/*
.text-slide-enter-from{
    transform: translateX(-200px);
    opacity: 0;
}
.text-slide-leave-to{
    transform: translateX(200px);
    opacity: 0;
}*/
.text :deep(.small-text){
        font-size:13px;
    }
</style>