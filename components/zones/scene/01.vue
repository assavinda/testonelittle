<template>
    <Container>

        <!-- Background -->
        <div>
            <img src="/public/images/zones/zones-bg.png" class="max-w-screen max-h-screen object-contain">
        </div>

        <!-- Girl -->
        <div class="absolute top-[0%] left-[39%] w-[72%]">
            <img src="/public/images/zones/girl.png">
        </div>

        <!-- Fan -->
        <div class="absolute top-[15%] left-[40.7%] w-[72%] zonemove">
            <img src="/public/images/zones/fan.png">
        </div>

        <!-- Girl Arms -->
        <div class="absolute top-[30%] left-[39.3%] w-[72.2%]">
            <img src="/public/images/zones/girl-arm.png">
        </div>

        <!-- Bow -->
        <div class="absolute top-[0%] left-[21%] w-[25%] bowmove">
            <img src="/public/images/zones/bow.png">
        </div>

        <!-- Bathtime Fun -->
        <div class="absolute top-[20%] left-[15%] w-[36%]">
            <button>
                <img src="/public/images/zones/bathtime.png">
            </button>
        </div>

        <!-- Super Relax -->
        <div class="absolute top-[50%] left-[15%] w-[36%]">
            <button @click="$emit('toCoffee01')">
                <img src="/public/images/zones/superrelax.png">
            </button>
        </div>

        <!-- Menu Icons -->
        <div class="absolute top-[2%] left-[2%] w-[7%]">
            <button>
                <img src="/public/images/general/home-icon.png">
            </button>
        </div>

        <div class="absolute top-[2%] left-[91%] w-[7%]">
            <img src="/public/images/general/info-icon.png">
        </div>

    </Container>
</template>

<script setup>

</script>

<style scoped>
@keyframes zoneicon {
    0% {
        rotate: 3deg;
    }
    100% {
        rotate: -3deg;
    }
}

@keyframes bow {
    0% {
        rotate: 5deg;
    }
    100% {
        rotate: 0deg;
    }
}

.zonemove {
    animation: zoneicon 1s infinite alternate ease-in-out;
    transform-origin: 50% 80%;
}

.bowmove {
    animation: bow 0.5s infinite alternate ease-in-out;
    transform-origin: center;
}
</style>