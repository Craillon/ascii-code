<template>
    <div>
        <div class="h-screen w-full relative">
            <div class="bg-white/80 backdrop-blur-md h-full w-full absolute bg-gradient-to-t z-30 from-white"></div>
            <div class="w-11/12 mx-auto h-full relative z-40">
                <div class="h-4/5 w-full flex items-center justify-center">
                    <div class="w-full text-center space-y-14">
                        <h4 class="text-2xl font-light text-green-700">Keyboard <span class="font-semibold text-slate-500">Game</span></h4>
                        <div class="flex items-center z-50">
                            <Vector class="absolut w-[30rem] mx-auto bg-white z-50 opacity-95" />
                        </div>
                    </div>
                </div>
                <div class=" flex items-center justify-center">
                    <NuxtLink to="/typing" class=" mb-10 bg-green-400 shadow-lg shadow-green-500/40 text-white hover:bg-green-400 bg-gradient-to-r hover:from-green-500 py-2 hover:shadow-xl hover:duration-700 rounded-full px-6">
                        Evaluez votre temps de saisie !
                    </NuxtLink>
                </div>
                <div class="absolute bottom-4 right-2">
                    <div class="text-xs">@Craillon > <span class="text-slate-300">Github | LinkedIn | TikTok</span></div>
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
    document.getElementById("audio").volume = 0.03
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