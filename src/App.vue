<script setup lang="js">
import { ref, onMounted, onUnmounted } from 'vue';

//navbar reactivity block
let egg = ref(false);
let homecoming = ref(false);
let homeClicks = ref(0);
let homeName = ref("Home");
function activateEgg() {
    document.title = "memory lane";
    egg.value = true;
}
function homeClick() {
    if (homeClicks.value == 2) {
        homeName.value = "Homecoming";
        homeClicks.value++;
    } else if (homeClicks.value == 3) {
        document.title = "do you think about me now and then"
        homecoming.value = true;
    } else {
        homeClicks.value++;
    }
}

// hero reactivity
let amazingQuotes = [
    "welcome to the greatest website on the internet",
    "hire me please, i want to buy a camaro",
    "bobcats for national title 2027",
    "stop looking at the best quotes ever and get back to work",
    "a probably-wise man once said, he who quotes others has no quotes of his own",
    "// TODO: add more quotes",
    "insert explosion here",
    "why is this not centeredㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ",
    "congratulations! you have just wasted 24 seconds of your life!",
    "patience"
];

let quoteIndex = 0;
let motd = ref(amazingQuotes[quoteIndex]);
let patienceActive = ref(false);
let quoteTimer;
onMounted(() => {
    quoteTimer = setInterval(() => {
        quoteIndex = (quoteIndex + 1) % amazingQuotes.length;
        motd.value = amazingQuotes[quoteIndex];
    }, 5_000);
});
onUnmounted(() => {
    clearInterval(quoteTimer);
});
function activatePatience() {
    patienceActive.value = true;
    document.title = "patience";
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 300ms ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

<template>
    <!-- if you're looking at this and arent me, you're a cheater. Otherwise, hello future caleb -->
    <div v-if="egg" class="min-h-screen w-full bg-black flex items-center justify-center flex-col">
        <!-- only the "real" ones will find the true meaning of the path -->
        <img src="./assets/tree.gif" title="MTAvMjMvMjAyNSAtIGlmIHRoZSBoaWdoZXIgaSBjbGltYiBpcyB0aGUgZnVydGhlciBpIGZhbGwsIHRoZW4gd2h5IGxvdmUgYW55dGhpbmcgYXQgYWxs">
        <p class="mt-2" title="09/05/2025">sometimes the best thing to do is to walk away.</p>
    </div>

    <div v-else-if="homecoming" class="min-h-screen w-full bg-black flex items-center justify-center flex-col">
        <img src="./assets/memory_lane.jpg">
        <div class="my-[1000px]"></div>
        <p>don't worry about me. you can stay however long you want.</p>
    </div>

    <div v-else-if="patienceActive" class="min-h-screen w-full bg-black flex flex-col items-center justify-center">
        <p class="text-white">just a little while longer.</p>
        <p>patience won't work this time. you can't ignore it anymore.</p>
        <p class="text-white">then, finally, it will be over.</p>
        <p>you know you can't win. might as well save time and get it over with.</p>
        <p class="text-white">i know it's a bad idea.</p>
        <p>just give up. like you always do, with everything else.</p>
        <p class="text-slate-400">you can do this. come on.</p>
        <p>but its true. if you would really get over it, then why am I still in your head? you know you can't shove me out. you've tried. i've watched you try.</p>
        <p class="text-slate-700">i can beat this. come on, cub. get up and walk away.</p>
        <p class="text-slate-700">just leave. it cant happen won't if you leave.</p>
        <p>but you know, deep down, that it will when you come back.</p>
        <p class="text-slate-800">i can't do it.</p>
        <p>then let me. it will only be, just a little while longer.</p>
        <p class="text-slate-900">fine. have your way.</p>
        <p>do not worry. it will all be over soon.</p>
    </div>

    <div v-else class="min-h-screen w-full bg-[#11111b] p-5 animate-fade-in">
        <!-- top bar -->
        <div class="p-1 sticky top-5 z-50 bg-[#1e1e2e] rounded">
            <div class="flex justify-between p-1 relative">
                <div class="text-[#cdd6f4] pl-2">
                    <b>Caleb Wietholter</b>
                </div>
                <div>
                    <a href="#top" class="py-1 px-4 rounded transition text-[#cdd6f4] hover:bg-[#313244]" @click="homeClick">{{ homeName }}</a>
                    <a href="#about" class="py-1 px-4 rounded transition text-[#cdd6f4] hover:bg-[#313244]">About Me</a>
                    <a href="#projects" class="py-1 px-4 rounded transition text-[#cdd6f4] hover:bg-[#313244]">Projects</a>
                </div>
                <div class="text-[#1e1e2e]">
                    <p @click="activateEgg" title="???" class="cursor-pointer text-xs">IaG</p>
                </div>
            </div>
        </div>

        <!-- hero -->
         <div class="bg-[#1e1e2e] mt-2.5 rounded p-5 min-h-[50vh] flex flex-col justify-center items-center">
            <h1 class="text-5xl text-[#cdd6f4]">Caleb Wietholter</h1>
            <Transition name="fade" mode="out-in">
               <a v-if="motd === 'patience'" key="patience-link" href="#" @click.prevent="activatePatience" class="text-[#cdd6f4] mt-3 underline">and sometimes, patience pays off</a>
               <i v-else key="quote-text" class="text-[#cdd6f4] mt-3">{{ motd }}</i>
            </Transition>
         </div>
    </div>
</template>