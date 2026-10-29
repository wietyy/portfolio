<script setup lang="js">
import { ref, onMounted, onUnmounted } from 'vue';

//navbar reactivity block
let egg = ref(false);
let homecoming = ref(false);
let homeClicks = ref(0);
let thisActive = ref(false);

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
    "patience", // trigger for "egg gyro"
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

function activateThis() {
    thisActive.value = true;
    document.title = "the other side";
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
        <img src="./assets/tree.gif"
            title="MTAvMjMvMjAyNSAtIGlmIHRoZSBoaWdoZXIgaSBjbGltYiBpcyB0aGUgZnVydGhlciBpIGZhbGwsIHRoZW4gd2h5IGxvdmUgYW55dGhpbmcgYXQgYWxs">
        <p class="mt-2" title="09/05/2025">sometimes the best thing to do is to walk away.</p>
    </div>

    <div v-else-if="homecoming" class="min-h-screen w-full bg-black flex items-center justify-center flex-col">
        <img src="./assets/memory_lane.jpg" title="memory lane">
        <div class="my-250"></div>
        <p>don't worry about me. you can stay however long you want.</p>
    </div>

    <div v-else-if="patienceActive" class="min-h-screen w-full bg-black flex flex-col items-center justify-center">
        <p class="text-white">just a little while longer.</p>
        <p>patience won't work this time. you can't ignore it anymore.</p>
        <p class="text-white">then, finally, it will be over.</p>
        <p>you know you can't win. might as well save time and get it over with.</p>
        <p class="text-white">you know it's a bad idea.</p>
        <p>just give up. like you always do, with everything else.</p>
        <p class="text-slate-400">you can do this. come on.</p>
        <p>but its true. if you would really get over it, then why am I still in your head? you know you can't shove me
            out. you've tried. i've watched you try.</p>
        <p class="text-slate-700">i can beat this. come on, cub. get up and walk away.</p>
        <p class="text-slate-700">just leave. it cant happen won't if you leave.</p>
        <p>but you know, deep down, that it will when you come back.</p>
        <p class="text-slate-800">i can't do it.</p>
        <p>then let me. it will only be, just a little while longer.</p>
        <p class="text-slate-900">fine. have your way.</p>
        <p>do not worry. it will all be over soon.</p>
    </div>

    <div v-else-if="thisActive" class="min-h-screen w-full bg-black flex justify-center items-center">
        <div class="text-white font-serif flex flex-col items-center">
            <p>Some things in a person's life are meant to go by unnoticed.</p>
            <p>Unseen, hidden behind the guise of something normal.</p>
            <p>Why then, I ask, are you here? To find secrets?</p>
            <p>Could be. Also could just be something put here to amuse you, to waste your time.</p>
            <p>Only I will ever know what I did. You, through hours of searching, will find only hints.</p>
            <p>You have your own secrets to guard. Things you would rather leave undiscovered.</p>
            <p class="text-black">.</p>
            <p>What are you doing here? You don't belong here!</p>
            <p class="text-blue-600 underline"><a href="https://uhsband.net">Back to Home</a></p>
        </div>
    </div>

    <div v-else class="min-h-screen p-3.5 bg-black text-white">
        <div id="top"></div>
        <!-- top bar -->
        <div class="sticky top-3.5 z-50 py-1.5 px-2 bg-[#111111] rounded-lg">
            <div class="grid grid-cols-[1fr_auto_1fr] items-center">
                <div class="justify-self-start pl-2 font-semibold text-[#fafafa]">
                    <b>Caleb Wietholter</b>
                </div>
                <div class="flex gap-1">
                    <a href="#top"
                        class="py-1.5 px-3 rounded-md text-sm font-medium text-[#a3a3a3] transition-colors hover:bg-[#1f1f1f] hover:text-[#fafafa]"
                        @click="homeClick">{{ homeName }}</a>
                    <a href="#about"
                        class="py-1.5 px-3 rounded-md text-sm font-medium text-[#a3a3a3] transition-colors hover:bg-[#1f1f1f] hover:text-[#fafafa]">About
                        Me</a>
                    <a href="#projects"
                        class="py-1.5 px-3 rounded-md text-sm font-medium text-[#a3a3a3] transition-colors hover:bg-[#1f1f1f] hover:text-[#fafafa]">Projects</a>
                    <a href="#contact"
                        class="py-1.5 px-3 rounded-md text-sm font-medium text-[#a3a3a3] transition-colors hover:bg-[#1f1f1f] hover:text-[#fafafa]">Contact</a>
                </div>
                <div class="justify-self-end">
                    <p @click="activateEgg" title="???" class="py-1.5 px-2 text-xs text-[#111111] cursor-pointer">IaG
                    </p>
                </div>
            </div>
        </div>

        <!-- hero -->
        <div
            class="mt-3.5 min-h-[90vh] p-5 bg-cover bg-center rounded-lg flex flex-col justify-center text-center bg-[url(./assets/fall.webp)]">
                <div class="self-center rounded-lg bg-[#111111] px-6 py-5">
                    <b class="block text-5xl text-white">Caleb Wietholter</b>
                    <Transition name="fade" mode="out-in">
                        <a v-if="motd === 'patience'" key="patience-link" href="#" @click.prevent="activatePatience"
                            class="mt-3 block text-base text-[#a3a3a3] underline cursor-pointer">and sometimes, patience pays off</a>
                        <i v-else :key="motd" class="mt-3 block text-base text-[#a3a3a3]">{{ motd }}</i>
                    </Transition>
                </div>
        </div>

        <!-- About Me -->
        <div id="about" class="mt-3.5 p-5 bg-[#111111] rounded-lg">
            <b class="block text-3xl text-white">About Me</b>
            <p class="mt-3 max-w-3xl leading-relaxed text-[#a3a3a3]">Welcome to what is commonly known as the greatest
                website you will ever visit. My name is Caleb Wietholter, and I will be your personal guide for your
                visit. I understand someone looking at this is most likely an interviewer, so I'll keep this quick. If,
                by chance, you are not an interviewer, kindly leave. Hosting is expensive nowadays.</p>

            <b class="block mt-8 text-xl text-white">Quick Facts</b>
            <ul class="mt-3 ml-5 list-disc space-y-1.5 text-[#a3a3a3]">
                <li>Birthplace: Morgantown, WV <i>(Take me home, country roads)</i></li>
                <li>Age: 18 years old (would give my birthday but that would help the identity thieves out there)</li>
                <li>Education: Currently a Freshman at Ohio University studying a dual major in Computer Science as well
                    as Artificial Intelligence</li>
            </ul>
            <p class="mt-5 max-w-3xl leading-relaxed text-[#a3a3a3]">But let's be real, who cares about that stuff? If
                you really are thinking about hiring me, here's the stuff you want to see:</p>
            <b class="block mt-8 text-xl text-white">Skills / My Stack</b>
            <ul class="mt-3 ml-5 list-disc space-y-1.5 text-[#a3a3a3]">
                <li class="mt-3 font-medium text-white">Programming Languages</li>
                <li class="ml-5">JavaScript (Primary)</li>
                <li class="ml-5">C++</li>
                <li class="ml-5">Rust</li>
                <li class="ml-5">Bit of experience with Python and Java</li>
                <li class="mt-3 font-medium text-white">Web Frameworks</li>
                <li class="ml-5">Vue.js (Preferred)</li>
                <li class="ml-5">React (Secondary)</li>
                <li class="mt-3 font-medium text-white">Databases</li>
                <li class="ml-5">PostgreSQL (Primary)</li>
                <li class="ml-5">MongoDB</li>
                <li class="ml-5">Redis</li>
                <li class="ml-5">SQLite (for edge development and on-device applications)</li>
                <li class="mt-3 font-medium text-white">Operating Systems</li>
                <img src="https://raw.githubusercontent.com/garrett/Tux/refs/heads/main/tux.svg" width="100"
                    alt="my goat tux the penguin" title="my goat tux the penguin" class="ml-5 mt-1">
                <li class="mt-3 font-medium text-white">Deployment Systems</li>
                <li class="ml-5">Docker / Podman</li>
                <li class="ml-5">(currently learning) Kubernetes</li>
                <li class="ml-5">GitHub Actions CI/CD</li>
                <li class="ml-5">(currently learning) Travis CI</li>
                <li class="mt-3 font-medium text-white">Other Skils</li>
                <li class="ml-5">Uses TailwindCSS</li>
                <li class="ml-5">Writes the majority of code myself</li>
                <li class="ml-5">...but does know how to effectively use AI-Assisted Development tools</li>
                <li class="ml-5">Magically gets stuff to work</li>
                <li class="ml-5">Can center a div (horizontally and vertically!)</li>
            </ul>
        </div>

        <!-- Projects section (here we go) -->
        <div id="projects" class="mt-3.5 p-5 bg-[#111111] rounded-lg">
            <b class="block text-3xl text-white">Projects</b>
            <p class="mt-3 text-[#a3a3a3]">Now <a @click="activateThis">THIS</a> is what you're here for.</p>
            <div class="mt-6 flex flex-wrap justify-center gap-6">
                <div
                    class="w-70 max-w-full aspect-9/16 flex flex-col overflow-hidden rounded-xl bg-[#171717] p-3">
                    <img src="./assets/john.png" alt="john demo image" class="h-44 w-full rounded-lg object-cover">
                    <div class="flex flex-col pt-3">
                        <b class="text-2xl text-center text-white">JOHN</b>
                        <i class="mt-2 text-sm leading-relaxed text-[#a3a3a3]">"An incredibly badass way to keep track
                            of your finances."</i>
                        <p class="mt-3 text-sm leading-relaxed text-[#a3a3a3]">Stack: Vite/React (Frontend),
                            Express/PostgreSQL (Backend)</p>
                        <p class="mt-2 text-sm leading-relaxed text-[#a3a3a3]">A fully-featured finance tracker app
                            inspired by my spreadsheet of 3+ years.</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Contact -->
        <div id="contact" class="mt-3.5 p-5 bg-[#111111] rounded-lg">
            <b class="block text-3xl text-white">Get in Touch</b>
            <div class="mt-6 flex flex-wrap gap-3">
                <a href="mailto:wietyy@outlook.com"
                    class="flex items-center gap-2 py-1.5 px-3 rounded-md text-sm font-medium text-[#a3a3a3] transition-colors hover:bg-[#1f1f1f] hover:text-[#fafafa]"><i
                        class="iconoir-mail" />Email</a>
                <a href="https://github.com/wietyy"
                    class="flex items-center gap-2 py-1.5 px-3 rounded-md text-sm font-medium text-[#a3a3a3] transition-colors hover:bg-[#1f1f1f] hover:text-[#fafafa]"><i
                        class="iconoir-github" />GitHub</a>
                <a href="https://www.youtube.com/watch?v=xvFZjo5PgG0"
                    class="flex items-center gap-2 py-1.5 px-3 rounded-md text-sm font-medium text-[#a3a3a3] transition-colors hover:bg-[#1f1f1f] hover:text-[#fafafa]"><i
                        class="iconoir-linkedin" />LinkedIn (soon)</a>
                <a href="https://raw.githubusercontent.com/wietyy/wietyy/main/resume.pdf"
                    class="flex items-center gap-2 py-1.5 px-3 rounded-md text-sm font-medium text-[#a3a3a3] transition-colors hover:bg-[#1f1f1f] hover:text-[#fafafa]"><i
                        class="iconoir-attachment" />Get my Resume</a>
            </div>
        </div>
    </div>
</template>
