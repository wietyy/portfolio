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
    "congratulations! you have just wasted 24 seconds of your life!"
];
let quoteIndex = 0;
let motd = ref(amazingQuotes[quoteIndex]);
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
         <div class="bg-[#1e1e2e] mt-2.5 rounded p-5 min-h-[50vh] flex flex-col justify-center items-center"> <!--tag-->
            <h1 class="text-5xl text-[#cdd6f4]">Caleb Wietholter</h1>
            <Transition name="fade" mode="out-in">
               <i :key="motd" class="text-[#cdd6f4] mt-3">{{ motd }}</i>
            </Transition>
         </div>
         <div class="min-h-[250vh]"></div>
    </div>
</template>