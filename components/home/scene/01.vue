<template>
    <Container>
        <div>
            <img src="/public/images/home/home-bg.png" class="max-w-screen max-h-screen object-contain">
        </div>

        <div class="absolute top-[13%] left-[41.5%] w-[37%] smokemove">
            <img src="/public/images/home/smoke.png">
        </div>

        <div class="absolute top-[27%] left-[5%] w-[47%]">
            <img src="/public/images/home/building-01.png">
        </div>

        <div class="absolute top-[24%] left-[50%] w-[47%] rotate-[5deg]">
            <img src="/public/images/home/building-02.png">
        </div>

        <div class="absolute top-[0%] left-[0%] w-[100%]">
            <img src="/public/images/home/homeground-bg.png">
        </div>

        <div class="absolute top-[31%] left-[25.5%] w-[47%]">
            <img src="/public/images/home/house.png">
        </div>

        <div class="absolute top-[35%] left-[50%] w-[65%] rotate-[5deg] car1move">
            <img src="/public/images/home/car-pink.png">
        </div>
        
        <div class="absolute top-[35%] left-[-10%] w-[67%] rotate-[5deg] car2move">
            <img src="/public/images/home/car-purple.png">
        </div>

        <div class="absolute top-[-4%] left-[29%] w-[40%] logo-move">
            <img src="/public/images/home/logo.png">
        </div>

        <div class="absolute top-[80%] left-[39%] w-[20%] playmove">
            <button @click="$emit('toZones')">
                <img src="/public/images/home/play-btn.png">
            </button>
        </div>
    </Container>
</template>

<script setup>

</script>

<style scoped>
@keyframes car1 {
    0% {
        rotate: -4deg;
    }
    100% {
        rotate: 4deg;
    }
}

@keyframes car2 {
    0% {
        rotate: 4deg;
    }
    100% {
        rotate: -4deg;
    }
}

@keyframes smoke {
    0% {
        transform: scaleY(1);
        translate: 0% 0%;
        opacity: 1;
    }
    100% {
        transform: scaleY(0.8);
        translate: 5% -1%;
        opacity: 0.25;
    }
}

@keyframes playbtn {
    0% {
        rotate: 2deg;
    }
    100% {
        rotate: -2deg;
    }
}

@keyframes logo {
    0% {
        transform: scale(1);
    }
    100% {
        transform: scale(1.05);
    }
}

.logo-move {
    animation: logo 0.5s infinite alternate ease-in-out;
    transform-origin: center;
}

.car1move {
    animation: car1 0.5s infinite alternate ease-in-out;
    transform-origin: center;
}

.car2move {
    animation: car2 0.5s infinite alternate ease-in-out;
    transform-origin: center;
}

.smokemove {
    animation: smoke 1s infinite ease-in-out;
    transform-origin: 0% 0%;
}

.playmove {
    animation: playbtn 0.2s infinite alternate ease-in-out;
    transform-origin: center;
}

.playmove:hover {
    width: 24%;
    top: 78%;
    left: 37%;
}
</style>