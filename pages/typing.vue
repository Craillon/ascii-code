<template>
    <div>
        <div class="h-screen w-full bg">
            <div class="bg-white/90 backdrop-blur-md h-full w-full absolute bg-gradient-to-t z-10 from-white"></div>
            <div class="w-11/12 mx-auto h-full relative z-50">
                <div class="">
                    <UDropdown  class="text-green-500 absolute z-50" :items="items" :ui="{ item: { disabled: 'cursor-text select-text' } }" :popper="{ placement: 'bottom-start' }">
                        <button type="button" class="bg-green-500 flex items-center gap-x-3 bg-gradient-to-r from-green-400 p-2 py-2.5 px-6 rounded shadow-lg mt-4 pr-6 shadow-green-500/40 text-white">
                            <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" viewBox="0 0 24 24">
                                <path fill-rule="evenodd" d="M18.425 10.271C19.499 8.967 18.57 7 16.88 7H7.12c-1.69 0-2.618 1.967-1.544 3.271l4.881 5.927a2 2 0 0 0 3.088 0l4.88-5.927Z" clip-rule="evenodd"/>
                            </svg>
                            {{ label }}
                        </button>
                        <!--  -->
                        <template #item="{ item }">
                            <span @click="changeLevel(item.label)" class="truncate text-slate-800 w-full h-full text-start"> {{ item.label }} </span>
                        </template>
                    </UDropdown>
                </div>
                <!--  -->
                <div class="h-2/5 w-full bg-slate-5 flex items-center justify-center relative">
                    <button type="button" @click="manupChrono()" class="absolute right-2 top-4 gap-x-4 flex items-center bg-green-500 bg-gradient-to-r from-green-400 p-2 rounded shadow-lg pr-6 shadow-green-500/40 text-white">
                        <div class="bg-white rounded-full text-green-500 h-8 w-8 flex items-center justify-center hover:shadow-lg duration-200">
                            <svg v-if="!startTime" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-4">
                                <path fill-rule="evenodd" d="M4.5 5.653c0-1.427 1.529-2.33 2.779-1.643l11.54 6.347c1.295.712 1.295 2.573 0 3.286L7.28 19.99c-1.25.687-2.779-.217-2.779-1.643V5.653Z" clip-rule="evenodd" />
                            </svg>
                            <svg v-else xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M15.75 5.25v13.5m-7.5-13.5v13.5" />
                            </svg>
                        </div>
                        <div class="flex items-baseline gap-4 relative">
                            <p class="w-11"><span class="text-xl font-medium">{{ chrono.M }}&nbsp;</span>min</p>
                            <p class="w-11"><span class="text-xl font-medium">{{ chrono.S }}&nbsp;</span>sec&nbsp;</p>
                            <p class="w-5 text-xl">{{ chrono.T !== 0 ? chrono.T : '00' }}</p>
                        </div>
                    </button>
                </div>
                <div v-if="worldTyping" class="h-2/5">
                    <!--  -->
                    <div class="h-2/4 flex items-center justify-center w-full  border-green-50 p-4 relative">
                        <p class="text text-slate-400 italic absolute -top-7 "> <span class="text-2xl">" </span>Text à saisir</p>
                        <p class="text-slate-500 text-xl">{{ lorem }}</p>
                    </div>
                    <!--  -->
                    <div class="h-2/4 w-11/12 mx-auto flex items-center justify-start">
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
                <div v-else class="h-2/5 bg-transparent bg-gradient-to-t from-slate-100/20 rounded-lg border-dashed">
                    <h3 class="text-slate-600 font-semibold text-center text-3xl">Partie terminée !</h3>
                    <div class="flex justify-center  w-full mt-10">
                        <a href="/typing" class="text-slate-800 rounded-full bg-green-200 p-1.5 px-6 shadow-green-100 shadow-md hover:bg-green-300 duration-300">Rejouez</a>
                    </div>
                </div>
                <div class="absolute left-0 right-0 bottom-0 flex items-center justify-center">
                    <a href="/" class=" mb-10 bg-slate-800 shadow-lg shadow-slate-500/30 text-white hover:bg-slate-700 py-2 hover:shadow-xl duration-300 rounded-full px-6">
                        Quittez la partie
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { faker } from '@faker-js/faker';

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


const label = ref("Difficulté")
const lorem = ref(faker.lorem.word())
const worldTyping = ref(lorem.value)
const value = ref("")
const index = ref(0);
const startTime = ref(false)
const chrono = ref({
    H: 0,
    M: 0,
    S: 0,
    T: 0,
})

const changeLevel = (data) => {
    label.value = data
    new Promise((resolve, reject) => setTimeout(resolve => {
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

    }, 100))
}

const manupChrono = () => {
    startTime.value = !startTime.value
}

onMounted(() => {
    window.addEventListener('keydown', ev => {
        startTime.value = true
        if (lorem.value.split('').at(index.value).charCodeAt(0) == ev.key.charCodeAt(0) || (lorem.value.split('').at(index.value -1) === "." && ev.key === " ") ) {
            value.value = ev.key
            worldTyping.value = worldTyping.value.split('').slice(1).join('')
            index.value++
        }
    })
    const id = setInterval(timerChrono, 1000/60);
    function timerChrono () {
        if (worldTyping.value.length === 0) {
            startTime.value = false
            clearInterval(id);
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
    

    // const id = setInterval(evnt => {timer.value = (timer.value++) / 60}, 100);
    // if (startTime) {
    //     function timerChrono() {
    //         if (worldTyping.value.length === 0) {
    //             if ( counter.value <= 0) {
    //                 startTime.value = false
    //                 clearInterval(id);
    //             } else {
    //                 timer.value = (timer.value++) / 60
    //             }
    //         }
    //     }
    // }


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