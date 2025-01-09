<template>
  <div class="flex h-screen w-screen bg-white place-items-center justify-center">

    <!-- Loading Background -->
    <div class="absolute">
      <Container>
        <img src="/public/images/general/loading-bg.png" class="max-w-screen max-h-screen object-contain">

        <div class="absolute top-[15%] left-[29%] w-[40%]">
            <img src="/public/images/home/logo.png">
        </div>

        <div class="absolute top-[55%] left-[41%] w-[40%]">
            <p class="loading-text text-responsive text-red-600">loading . . .</p>
        </div>

      </Container>
    </div>

    <!-- Home Scene -->
    <div v-if="currentScene === 'Home'" class="absolute">
      <HomeScene01 @toZones="setScene('Zones')"></HomeScene01>
    </div>

    <!-- Zones Scene -->
    <div v-if="currentScene === 'Zones'" class="absolute">
      <ZonesScene01 @toCoffee01="setScene('Coffee01')"></ZonesScene01>
    </div>

    <!-- Coffee Scene -->
    <div v-if="currentScene === 'Coffee01'" class="absolute">
      <CoffeeGameScene01 @nextgame="setScene('testdraw')"></CoffeeGameScene01>
    </div>

    <!-- testdraw -->
    <div v-if="currentScene === 'testdraw'" class="absolute">
      <TestdrawScene2></TestdrawScene2>
    </div>

    <div v-if="currentScene === 'Coffee02'" class="absolute">
      <CoffeeGameScene02></CoffeeGameScene02>
    </div>

  </div>
</template>


<script setup>

// Current Scene State
const currentScene = ref('Coffee01');

// Change Scenes Function
function setScene(sceneName) {
  currentScene.value = sceneName;
}

</script>


<style>
body {
  overflow: hidden;
}

.loading-text {
    font-family: 'wintermouse', sans-serif;
}

.text-responsive {
    font-size: 7vh;
}

@media (max-aspect-ratio: 16/9) {

.text-responsive {
    font-size: 3.9375vw;
}

}
</style>

