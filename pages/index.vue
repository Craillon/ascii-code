<template>
    <div>
        <div class="h-screen w-full ">
            <div class="w-11/12 mx-auto h-full relative">
                <div class="h-4/5 w-full flex items-center justify-center">
                    <div class="w-full text-center space-y-16">
                        <h4 class="font-medium text-6xl text-green-600">Keyboard <span class="p-3 rounded-lg bg-amber-300/20 text-slate-700">Game</span></h4>
                        <img src="~/assets/images/schema_azerty_dactylo_nb_1800x1084.png" alt="" class="w-4/12 mx-auto">
                        <!-- <p class="text-slate-500">Calculez votre temps de saisi !</p> -->
                    </div>
                </div>
                <div class="absolute left-0 right-0 bottom-0 flex items-center justify-center">
                    <NuxtLink to="/typing" class=" mb-10 bg-green-400 shadow-lg shadow-green-500/40 text-white hover:bg-green-400 py-3 hover:shadow-xl duration-300 rounded-full px-6">
                        Calculez votre temps de saisi !
                    </NuxtLink>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>

</style>