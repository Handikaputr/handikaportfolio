<script setup>
    import About from '@/component/homePage/about.vue';
import Beranda from '@/component/homePage/beranda.vue';
import Project from '@/component/homePage/project.vue';
import navigation from '@/component/navigation.vue';
</script>
<template>
    <navigation></navigation>
    <div class="main main w-screen flex flex-col items-center overflow-x-hidden min-h-screen">
    <Beranda></Beranda>
    <About></About>
    <Project></Project> 
    </div>
</template>
