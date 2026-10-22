<script setup lang="js">
import { ref } from 'vue';

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
</script>

<template>
    <!-- if you're looking at this and arent me, you're a cheater. Otherwise, hello future caleb -->
    <div v-if="egg" class="min-h-screen w-full bg-black flex items-center justify-center flex-col">
        <!-- only the "real" ones will find the true meaning of the path -->
        <img src="./assets/tree.gif" title="MTAvMjMvMjAyNSAtIGlmIHRoZSBoaWdoZXIgaSBjbGltYiBpcyB0aGUgZnVydGhlciBpIGZhbGwsIHRoZW4gd2h5IGxvdmUgYW55dGhpbmcgYXQgYWxs">
        <p class="mt-2" title="09/05/2025">sometimes the best thing to do is to walk away.</p>
    </div>

    <div v-if="homecoming" class="min-h-screen w-full bg-black flex items-center justify-center flex-col">
        <img src="./assets/memory_lane.jpg">
        <div class="my-[1000px]"></div>
        <p>don't worry about me. you can stay however long you want.</p>
    </div>

    <!-- top bar -->
    <div v-else class="min-h-screen w-full bg-[#11111b] p-5 animate-fade-in">
        <div class="p-1 bg-[#1e1e2e] rounded">
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
    </div>
</template>