<script setup>
import { ref } from 'vue';
const navCondition = ref(false);
const exitClassLeft = "animate__fadeOutLeft";
const exitClassRight = "animate__fadeOutRight";

function navClickMain() {
        navCondition.value = !navCondition.value;
}
</script>
<template>
    <div id="main-nav"
        :class="navCondition ? 'w-full' : 'w-12'"
        class="nav z-40 fixed bottom-4 right-1/2 text-2xl duration-1000 flex  translate-x-1/2 main-nav max-w-96 text-white shadow-purple h-12  items-center justify-center rounded-full bg-purple-600">
        <a :class="navCondition ? 'animate__fadeInRight' : exitClassRight" class=" flex-1 items-center flex justify-center animate__animated left duration-150 main-nav-item" href="#home"><ion-icon
                   class="main-nav-icon bg-purple-600" name="home"></ion-icon></a>
        <a :class="navCondition ? 'animate__fadeInRight' : exitClassRight" class=" flex-1 items-center flex justify-center animate__animated left duration-150 main-nav-item" href="#about"><ion-icon
                class="main-nav-icon bg-purple-600" name="person"></ion-icon></a>
        <button @click="navClickMain"
            class="w-10 flex-0 h-10 z-10 flex items-center justify-center bg-white border-4 hover:rotate-90 shadow-md duration-200 border-white rounded-full text-slate-600"><ion-icon
                name="close"></ion-icon></button>
        <a :class="navCondition ? 'animate__fadeInLeft' : exitClassLeft" class=" flex-1 items-center flex justify-center animate__animated duration-150 main-nav-item" href="#project">
        <ion-icon class="main-nav-icon bg-purple-600" name="images"></ion-icon></a>
        <a :class="navCondition ? 'animate__fadeInLeft' : exitClassLeft" class=" flex-1 items-center flex justify-center animate__animated duration-150 main-nav-item" href="#archivement"><ion-icon
                class="main-nav-icon bg-purple-600" name="medal"></ion-icon></a>
    </div>
</template>