<template>
    <div>
        <div class="h-screen w-full bg">
            <div class="bg-white/95 backdrop-blur-md h-full w-full absolute bg-gradient-to-t z-10 from-white"></div>
            <div class="w-11/12 mx-auto h-full relative z-40">
                <!--  -->
                <div v-if="worldTyping" class="absolute top-3 z-40 w-8/12 mx-auto grid grid-cols-4 gap-x-4 left-0 right-0">
                    <div class="col-span-1 bg-white border-slate-300 p-2 rounded flex items-center gap-7">
                        <div class="text-slate-500 p-2">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M6.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM12.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0ZM18.75 12a.75.75 0 1 1-1.5 0 .75.75 0 0 1 1.5 0Z" />
                            </svg>
                        </div>
                        <div class="">
                            <h5 class="text-2xl">
                                <p>{{ lorem.length }}</p>
                                <p class="text-xs font-normal">{{ lorem.length > 1 ? 'caractères' : 'caractère' }}</p>
                            </h5>
                        </div>
                    </div>
                    <!--  -->
                    <div class="col-span-1 bg-white border-slate-300 p-2 rounded flex items-center gap-7">
                        <div class="text-slate-500 rounded p-2">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25H12" />
                            </svg>
                        </div>
                        <div class="">
                            <h5 class="text-2xl">
                                <p>{{ lorem.split(' ').length }}</p>
                                <p class="text-xs font-normal">{{ lorem.split(' ').length > 1 ? 'mots' : 'mot'}}</p>
                            </h5>
                        </div>
                    </div>
                    <!--  -->
                    <div class="col-span-2 relative bg-white border-slate-300 p-2 px-4 rounded flex items-center justify-center gap-7">
                        <button type="button" @click="manupChrono()" class="absolute left-6 top-2.5 gap-x-4 flex items-center rounded bg-white text-white">
                            <div class="bg-white rounded-full text-green-500 h-10 w-10 flex items-center justify-center  shadow-slate-300/25 duration-200">
                                <svg v-if="!startTime" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-4">
                                    <path fill-rule="evenodd" d="M4.5 5.653c0-1.427 1.529-2.33 2.779-1.643l11.54 6.347c1.295.712 1.295 2.573 0 3.286L7.28 19.99c-1.25.687-2.779-.217-2.779-1.643V5.653Z" clip-rule="evenodd" />
                                </svg>
                                <svg v-else xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                                    <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 5.25v13.5m-7.5-13.5v13.5" />
                                </svg>
                            </div>
                        </button>
                        <div class="flex items-baseline gap-4 relative justify-center text-slate-600">
                            <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
                                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"/>
                            </svg>
                            <p class="w-11"><span class="text-xl font-medium">{{ chrono.M }}&nbsp;</span>min</p>
                            <p class="w-11"><span class="text-xl font-medium">{{ chrono.S }}&nbsp;</span>sec&nbsp;</p>
                            <p class="w-10 text-center text-xl">{{ chrono.T !== 0 ? chrono.T : '00' }}</p>
                        </div>
                    </div>
                </div>
                <!-- LEVEL MODAL -->
                <div v-if="worldTyping" class="">
                    <UDropdown  class="text-green-500 absolute -right-8 z-50" :items="items" :ui="{ item: { disabled: 'cursor-text select-text' } }" :popper="{ placement: 'bottom-start' }">
                        <button type="button" class="bg-green-500 h- flex items-center gap-x-3 bg-gradient-to-r from-green-400 p-3 rounded shadow mt-4 shadow-green-500/40 text-white">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
                            </svg>
                            <!-- {{ label }} -->
                        </button>
                        <!--  -->
                        <template #item="{ item }">
                            <a :href="`/typing#${item.label}`" @click="changeLevel(item.label)" class="truncate text-slate-800 w-full h-full text-start"> {{ item.label }} </a>
                        </template>
                    </UDropdown>
                </div>
                <!-- TEXT TYPING -->
                <div v-if="worldTyping" class="h-4/5 block space-y-3">
                    <!--  -->
                    <div class="h-4/5 flex items-end justify-center w-full  border-green-50 p-4 relative">
                        <p class="text-slate-500 text-xl bg-slate-50 p-1">{{ lorem }}</p>
                    </div>
                    <!--  -->
                    <div class="h-1/5 w-11/12 mx-auto flex items-center justify-start">
                        <div class="text-xl text-nowrap overflow-hidden relative" >
                            <div class="ml-[37rem] text-white space-x-2 flex items-center p-8">
                                <template v-for="(item, idx) in worldTyping.split('')" :key="idx" class="p-2">
                                    <span v-if=" idx === 0 " class="bg-green-400 p-2 h-14 px-4 shadow-lg shadow-green-400/50 rounded text-2xl font-bold duration-150">{{ item }}</span>
                                    <span v-else class="bg-slate-100 rounded h-11 px-2.5 duration-150 p-2 text-slate-800">{{ item }}</span>
                                </template>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- WIN POPUP -->
                <div v-else class="h-full re absolute flex items-center justify-center left-0 right-0 w-full z-50 bg-gradient-to-t my-auto from-slate-100/20">
                    <div class="h-4/6 relative w-7/12 ">
                        <img src="~/assets/images/Bingo-pana.png" alt="success image" class="w-60 mx-auto bg-slate-50/50 rounded">
                        <h3 class="text-slate-600 font-semibold text-center text-3xl">Partie terminée !</h3>
                        <div class="">
                            <p class="text-xs mt-6 text-center">
                                Vous avez terminé la partie de <span class="font-bold">{{ lorem.split(' ').length > 1 ? lorem.split(' ').length+' mots' : lorem.split(' ').length+' mot' }} </span>
                                contant <span class="font-bold">{{ lorem.length > 1 ? lorem.length+' caractères' : lorem.length+' caractère' }}</span> avec succès ! <br>votre score est de
                                <span class="font-bold">{{ `${chrono.H} heure ${chrono.M} min ${chrono.S} sec ${chrono.T} tier` }}</span>
                            </p>
                        </div>
                        <div class="flex justify-center w-full my-10">
                            <a :href="`#${level}`" @click="newParty(level)" class="text-slate-800 rounded-full bg-green-200 p-1.5 px-6 shadow-green-100 shadow-md hover:bg-green-300 duration-300">Rejouez</a>
                        </div>
                    </div>
                    <div class="absolute top-1 flex items-center justify-center mt-8 gap-x-8">
                            <a v-for="(item, index) in items[0]" :key="index" :href="`#${item.label}`" @click="changeLevel(item.label)" class="text-xs py-1 hover:text-green-400 duration-300">{{ item.label }}</a>
                    </div>
                </div>
                <!-- EXIT BTN -->
                <div class="absolute z-50 left-0 right-0 bottom-0 flex items-center justify-center">
                    <a href="/" class=" mb-10 bg-slate-800 shadow-lg shadow-slate-500/30 text-white hover:bg-slate-700 py-2 hover:shadow-xl duration-300 rounded-full px-6">
                        Quittez la partie
                    </a>
                </div>
            </div>
        </div>
        <audio id="audio" class="hidden">
            <source src="~/assets/audio/mechanical-keyboard-sounds-gaming-on-a-keyboard-17149 (2).mp3" type="audio/ogg">
            <source src="~/assets/audio/mechanical-keyboard-sounds-gaming-on-a-keyboard-17149 (2).mp3" type="audio/mpeg">
            Your browser does not support the audio element.
        </audio>
        <audio autoplay id="fond-sonor" class="hidden">
            <source src="~/assets/audio/Louis Adrien - Escape to Sicily_Instrumental.mp3" type="audio/ogg">
            <source src="~/assets/audio/Louis Adrien - Escape to Sicily_Instrumental.mp3" type="audio/mpeg">
            Your browser does not support the audio element.
        </audio>
    </div>
</template>

<script setup>
import { faker } from '@faker-js/faker';
const inc = ref(0)
const func = () => inc.value++

const items = [
    [
        { label: 'Mot' },
        { label: 'Mots' },
        { label: 'Phrase' },
        { label: 'Phrases' },
        { label: 'Ligne' },
        { label: 'Paragraphe' },
        { label: 'Paragraphes' },
        { label: 'Text' }
    ]
]

const level = ref("")

const label = ref("")
const lorem = ref("")
const worldTyping = ref(".")
const value = ref("")
const index = ref(0);
const startTime = ref(false)
const chrono = ref({
    H: 0,
    M: 0,
    S: 0,
    T: 0,
})

const idInterval = ref()

const newParty = () => {
    changeLevel('Mot')
}

const changeLevel = (data) => {
    label.value = data
    if (data == "Mot") {
        lorem.value = faker.lorem.word()
        worldTyping.value = lorem.value
    }
    if (data == "Mots") {
        lorem.value = faker.lorem.words()
        worldTyping.value = lorem.value
    }
    if (data == "Phrase") {
        lorem.value = faker.lorem.sentence()
        worldTyping.value = lorem.value
    }
    if (data == "Phrases") {
        lorem.value = faker.lorem.sentences()
        worldTyping.value = lorem.value
    }
    if (data == "Ligne") {
        lorem.value = faker.lorem.line()
        worldTyping.value = lorem.value
    }
    if (data == "Lignes") {
        lorem.value = faker.lorem.lines()
        worldTyping.value = lorem.value
    }
    if (data == "Paragraphe") {
        lorem.value = faker.lorem.paragraph()
        worldTyping.value = lorem.value
    }
    if (data == "Paragraphes") {
        lorem.value = faker.lorem.paragraphs()
        worldTyping.value = lorem.value
    }
    if (data == "Text") {
        lorem.value = faker.lorem.text()
        worldTyping.value = lorem.value
    }
    localStorage.setItem("level", data)
    clearInterva(idInterval.value)
    resetChrono()
}

const manupChrono = () => {
    startTime.value = !startTime.value
}

const windowEvent = () => {
    window.addEventListener('keydown', ev => {
        startTime.value = true
        if (lorem.value.split('').at(index.value).charCodeAt(0) == ev.key.charCodeAt(0) || (lorem.value.split('').at(index.value -1) === "." && ev.key === " ") ) {
            document.getElementById("audio").play()
            value.value = ev.key
            worldTyping.value = worldTyping.value.split('').slice(1).join('')
            index.value++
        }
        if (worldTyping.value.length === 0) {
            // Code pour bloquer la modal de message success
        }
    })
}

const timerChrono = () => {
    if (worldTyping.value.length === 0 ) {
        clearInterva(idInterval.value);
    } else {
        if (startTime.value == true) {
            chrono.value.T++ 
            if (chrono.value.T === 60) {
                chrono.value.S++
                if (chrono.value.S == 60) {
                    chrono.value.M++
                    chrono.value.S = 0
                    if (chrono.value.M == 60) {
                        chrono.value.H++
                        chrono.value.M = 0
                    }
                }
                chrono.value.T = 0
            }
        }
    }
}

const intervalChrono = () => setInterval(timerChrono, 1000/60);

const clearInterva = (id) => {
    startTime.value = false
    clearInterval(id)
}

const resetChrono = () => {
    chrono.value.H = 0;
    chrono.value.M = 0;
    chrono.value.S = 0;
    chrono.value.T = 0
}

onBeforeRouteUpdate( (from, to) => {
    index.value = 0
    resetChrono()
    windowEvent()
    idInterval.value = intervalChrono()
})

onBeforeMount(() => {
    level.value = !!localStorage.getItem("level") ? localStorage.getItem("level") : "Mot"
    changeLevel(level.value)
    worldTyping.value = lorem.value
    windowEvent()
    idInterval.value = intervalChrono()
})

onMounted(() => {
    const fondSonor = document.getElementById("fond-sonor")
    fondSonor.autoplay = true
    fondSonor.volume = 0.005
    fondSonor.loop = true
})

</script>

<style scoped>
.bg {
    background: url("~/assets/images/bg-background.jpg");
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
}
</style>