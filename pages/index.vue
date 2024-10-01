<template>
    <div>
        <div class="h-screen w-full relative">
            <!-- <a href="https://github.com/Craillon/ascii-code" class="absolute top-2 right-2 text-xs z-50 py-1 rounded-full mr-10 mt-3 text-white pr-4 pl-2 shadow-md flex items-center gap-x-2 bg-slate-800">
                <svg class="w-6 h-6" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="currentColor" viewBox="0 0 24 24">
                    <path fill-rule="evenodd" d="M12.006 2a9.847 9.847 0 0 0-6.484 2.44 10.32 10.32 0 0 0-3.393 6.17 10.48 10.48 0 0 0 1.317 6.955 10.045 10.045 0 0 0 5.4 4.418c.504.095.683-.223.683-.494 0-.245-.01-1.052-.014-1.908-2.78.62-3.366-1.21-3.366-1.21a2.711 2.711 0 0 0-1.11-1.5c-.907-.637.07-.621.07-.621.317.044.62.163.885.346.266.183.487.426.647.71.135.253.318.476.538.655a2.079 2.079 0 0 0 2.37.196c.045-.52.27-1.006.635-1.37-2.219-.259-4.554-1.138-4.554-5.07a4.022 4.022 0 0 1 1.031-2.75 3.77 3.77 0 0 1 .096-2.713s.839-.275 2.749 1.05a9.26 9.26 0 0 1 5.004 0c1.906-1.325 2.74-1.05 2.74-1.05.37.858.406 1.828.101 2.713a4.017 4.017 0 0 1 1.029 2.75c0 3.939-2.339 4.805-4.564 5.058a2.471 2.471 0 0 1 .679 1.897c0 1.372-.012 2.477-.012 2.814 0 .272.18.592.687.492a10.05 10.05 0 0 0 5.388-4.421 10.473 10.473 0 0 0 1.313-6.948 10.32 10.32 0 0 0-3.39-6.165A9.847 9.847 0 0 0 12.007 2Z" clip-rule="evenodd"/>
                </svg>
                Github
            </a> -->
            <!-- <a href="https://github.com/Craillon/ascii-code" class="absolute right-3 top-3 z-50">Moi aussi je suis un lien</a> -->
            <div class="bg-white/80 backdrop-blur-md h-full w-full absolute bg-gradient-to-t z-30 from-white"></div>
            <div class="w-11/12 mx-auto h-full relative z-40">
                <div class="h-4/5 w-full flex items-center justify-center">
                    <div class="w-full text-center space-y-14">
                        <h4 class="text-2xl font-light text-green-700">Keyboard <span class="font-semibold text-slate-500">Game</span></h4>
                        <img src="~/assets/images/1_BbDBPnpY_yt1q7CXtsYEJg.jpg" alt="" class="w-4/12 mx-auto mt-5">
                    </div>
                </div>
                <div class="absolute left-0 right-0 bottom-10 flex items-center justify-center">
                    <NuxtLink to="/typing" class=" mb-10 bg-green-400 shadow-lg shadow-green-500/40 text-white hover:bg-green-400 bg-gradient-to-r hover:from-green-500 py-2 hover:shadow-xl hover:duration-700 rounded-full px-6">
                        Calculez votre temps de saisie !
                    </NuxtLink>
                </div>
            </div>
        </div>
        <audio id="audio" autoplay controls class="hidden">
            <source src="~/assets/audio/keyboard-sound-200501_UtkGUmJX.mp3" type="audio/ogg">
            <source src="~/assets/audio/keyboard-sound-200501_UtkGUmJX.mp3" type="audio/mpeg">
            Your browser does not support the audio element.
        </audio>
    </div>
</template>

<script setup>
onMounted(() => {
    window.addEventListener('load',  ev => {
        document.getElementById("audio").autoplay = true
    })
});
</script>

<style scoped>
.bg {
    background: url("~/assets/images/bg-background.jpg");
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
}
</style>