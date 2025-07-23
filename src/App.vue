<template>
  <div id="app">
    <HeaderBar @navigate="handleNavigation"/>
    <section class="screen" id="screen1"><BannerSection /></section> 
    <section class="screen with-bg" id="screen2"><AboutSection /></section>
    <section class="screen with-bg" id="screen3"><TeamSection/></section>
    <section class="screen with-bg" id="screen4"><JobSection/></section>
    <FooterSection />
  </div>
</template>

<script setup>
import HeaderBar from './components/HeaderBar.vue'
import BannerSection from './components/BannerSection.vue'
import AboutSection from './components/AboutSection.vue'
import TeamSection from './components/TeamSection.vue';
import JobSection from './components/JobSection.vue';
import FooterSection from './components/FooterSection.vue';

/* 滚轮监听切换屏幕 */
import{onMounted,onUnmounted}from'vue'

let index=0;
const total=5;
let throttle=false;

function handleHeaderClass(newIndex){
  const header=document.getElementById("mainheader");
  if(header){
    if(newIndex>0){
      header.classList.add('active');
    }else{
      header.classList.remove('active');
    }
  }
}

function handleNavigation(targetIndex){
  if(index!=targetIndex){
    index=targetIndex;
    scrollTo(index);
    handleHeaderClass(index);
  }
}

function scrollTo(index){
  const section=document.querySelector(`#screen${index+1}`)
  section?.scrollIntoView({behavior:'smooth'})
}

function onWheel(e){
  if(index==total-1&&e.deltaY>0)return;
  if(throttle)return
  throttle=true
  if(e.deltaY>0&&index<total-1)index++
  else if(e.deltaY<0&&index>0)index--
  scrollTo(index);
  handleHeaderClass(index);
  setTimeout(()=>{throttle=false},800)
}

onMounted(()=>{
  window.addEventListener('wheel',onWheel)
  handleHeaderClass(index);
})
onUnmounted(()=>{
  window.removeEventListener('wheel',onWheel)
})


</script>

<style>
html,body {
  margin: 0;
 /* overflow: hidden;*/
  scroll-behavior: smooth;
  font-family: "Microsoft YaHei", sans-serif;
}
.container{
  height: 100vh;
  overflow: hidden;
}
.screen{
  height: 100vh;
  scroll-snap-align: start;
}
.with-bg{
  background-image: url('/bkgr.png');
  background-position: center;
  background-attachment: fixed;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
