<template>
    <div>
        <div class="h-screen w-full ">
            <div class="w-11/12 mx-auto h-full relative">
                <div class="h-2/5 w-full bg-slate-50 flex items-center justify-center">
                    <p class="mt-10 text-xl">{{ world }} ++ {{ lorem.length }} ++ {{ index }}</p>
                </div>
                <div class="h-1/5 flex items-center justify-center w-full bg-slate-50 p-4">
                    <p class="">{{ lorem }}</p>
                </div>
                <div class="h-1/5 w-11/12 mx-auto flex items-center justify-center">
                    <div class="text-xl text-nowrap overflow-hidden relative" >
                        {{ worldTyping }}
                    </div>
                </div>
                <div class="absolute left-0 right-0 bottom-0 flex items-center justify-center">
                    <button class=" mb-10 bg-green-300/40 shadow hover:shadow-md duration-300 rounded-full px-6 py-1">Start party</button>
                </div>
            </div>
        </div>
        <input v-model="value" @input="typingAsciiCode()" type="text" v-focus class="absolute bottom-0 opacity-0 py-1 text-center border bg-emerald-400 w-full">
    </div>
</template>

<script setup>
import { faker } from '@faker-js/faker';


const lorem = ref(faker.lorem.lines())
// const lorem = ref("faker")
const index = ref(0)
const vFocus = { mounted: (el) => el.focus() }
const value = ref("")
const warning = ref(false)
const world = ref("No")
const worldTyping = ref("")


const typingAsciiCode = () => {
    // reinitValue()
    if ( index.value <= lorem.value.split('').length ) {
        if (value.value.length == 1) {
            value.value = value.value.split('').at(0)
        }else {
            value.value = value.value.split('').at(1)
        }
    } else {
        value.value = value.value.split('').at(0)
    }
    
    
    if (lorem.value.split('').at(index.value) == value.value) {
        index.value++
        world.value = "OK"
        worldTyping.value += value.value
        return
    }
    world.value = "NON"
}

onMounted(() => {
    
})
</script>

<style lang="scss" scoped>

</style>