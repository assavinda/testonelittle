<template>
    <Container ref="container">
        <!-- Background -->
        <div>
            <img src="/public/images/coffee-game-02/bg-coffee-game02.png" class="max-w-screen max-h-screen object-contain">
        </div>

        <!-- Drawing Canvas -->
        <canvas
          ref="drawingCanvas"
          @mousedown="startDrawing"
          @mousemove="draw"
          @mouseup="stopDrawing"
          @mouseleave="stopDrawing"
          @touchstart="startDrawing"
          @touchmove="draw"
          @touchcancel="stopDrawing"
          @touchend="stopDrawing"
          class="absolute top-[40%] left-[35%]" :style="{width: canvasWidth + '%', height: canvasHeight + '%'}"
        ></canvas>

        <!-- Controls -->
        <div class="controls absolute top-0 right-0 p-4">
          <label>
            Brush Size:
            <input type="range" min="1" max="20" v-model="brushSize" />
          </label>
          <label>
            Brush Color:
            <input type="color" v-model="brushColor" />
          </label>
          <button @click="clearCanvas">Clear</button>
        </div>

    </Container>
</template>

<script setup>
const drawingCanvas = ref(null);
const isDrawing = ref(false);
const brushSize = ref(3);
const brushColor = ref('#000000');
const context = ref(null);
const canvasWidth = ref(30);
const canvasHeight = ref(30);

let drawingCanvasBound = null


onMounted(() => {
  const canvas = drawingCanvas.value;
  context.value = canvas.getContext('2d');
  context.value.lineCap = 'round';
});

function getBound() {
    const drawingCanvasElement = drawingCanvas.value?.$el || drawingCanvas.value;
    drawingCanvasBound = drawingCanvasElement.getBoundingClientRect();
}

function startDrawing(e) {
  isDrawing.value = true;

  drawingCanvasBound == null ? getBound() : console.log('gotten');

  context.value.beginPath();
  const clientX = e.touches ? e.touches[0].clientX : e.clientX;
  const clientY = e.touches ? e.touches[0].clientY : e.clientY;
  const pcX = (clientX - drawingCanvasBound.left) / drawingCanvasBound.width * 100;
  const pcY = (clientY - drawingCanvasBound.top) / drawingCanvasBound.height * 100;
  context.value.moveTo(pcX*3, pcY*1.5);
  console.log(pcX, pcY);

};

function draw(e) {
  if (!isDrawing.value) return;
  const clientX = e.touches ? e.touches[0].clientX : e.clientX;
  const clientY = e.touches ? e.touches[0].clientY : e.clientY;
  const pcX = (clientX - drawingCanvasBound.left) / drawingCanvasBound.width * 100;
  const pcY = (clientY - drawingCanvasBound.top) / drawingCanvasBound.height * 100;
  context.value.lineTo(pcX*3, pcY*1.5);

  console.log(pcX, pcY);

  context.value.strokeStyle = brushColor.value;
  context.value.lineWidth = brushSize.value;
  context.value.stroke();
};

function stopDrawing() {
  isDrawing.value = false;
  context.value.closePath();
};

function clearCanvas() {
  context.value.clearRect(0, 0, drawingCanvas.value.width, drawingCanvas.value.height);
};

</script>

<style scoped>

</style>