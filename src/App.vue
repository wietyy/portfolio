<script setup lang="js">
import { ref } from 'vue';
let egg = ref(false);

function activateEgg() {
    egg.value = true;
}
</script>

<template>
    <!-- if you're looking at this and arent me, you're a cheater. Otherwise, hello future caleb -->
    <div v-if="egg">
        <iframe src="https://deltarune.com/man" class="min-h-screen w-full border-0" frameborder="0"></iframe>
    </div>

    <!-- top bar -->
    <div v-else class="min-h-screen w-full bg-[#11111b] p-5 animate-fade-in">
        <div class="p-1 bg-[#1e1e2e] rounded">
            <div class="flex justify-between p-1 relative">
                <div class="text-[#cdd6f4] pl-2">
                    <b>Caleb Wietholter</b>
                </div>
                <div>
                    <a href="#top" class="py-1 px-4 rounded transition text-[#cdd6f4] hover:bg-[#313244]">Home</a>
                    <a href="#about" class="py-1 px-4 rounded transition text-[#cdd6f4] hover:bg-[#313244]">About Me</a>
                    <a href="#projects" class="py-1 px-4 rounded transition text-[#cdd6f4] hover:bg-[#313244]">Projects</a>
                </div>
                <div class="text-[#1e1e2e]">
                    <p @click="activateEgg" class="cursor-pointer">???</p>
                </div>
            </div>
        </div>
    </div>
</template>