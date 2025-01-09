<template>
    <div class="drawing-app">
      <div class="canvas-container">
        <canvas
          ref="drawingCanvas"
          @mousedown="startDrawing"
          @mousemove="draw"
          @mouseup="stopDrawing"
          @mouseleave="stopDrawing"
        ></canvas>
      </div>
      <div class="controls">
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
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        isDrawing: false,
        brushSize: 5,
        brushColor: '#000000',
        context: null,
        canvasWidth: 0,
        canvasHeight: 0,
      };
    },
    mounted() {
      const canvas = this.$refs.drawingCanvas;
      this.setCanvasSize();
      this.context = canvas.getContext('2d');
      this.context.lineCap = 'round';
  
      // Redraw canvas contents when resizing
      window.addEventListener('resize', this.onResize);
    },
    beforeDestroy() {
      window.removeEventListener('resize', this.onResize);
    },
    methods: {
      setCanvasSize() {
        const canvas = this.$refs.drawingCanvas;
        const container = canvas.parentElement;
  
        // Set canvas size to match container size
        canvas.width = container.offsetWidth;
        canvas.height = container.offsetHeight;
  
        this.canvasWidth = canvas.width;
        this.canvasHeight = canvas.height;
      },
      onResize() {
        // Save current canvas content
        const tempCanvas = document.createElement('canvas');
        tempCanvas.width = this.canvasWidth;
        tempCanvas.height = this.canvasHeight;
        const tempContext = tempCanvas.getContext('2d');
        tempContext.drawImage(this.$refs.drawingCanvas, 0, 0);
  
        // Resize canvas and redraw saved content
        this.setCanvasSize();
        this.context.drawImage(tempCanvas, 0, 0, this.canvasWidth, this.canvasHeight);
      },
      startDrawing(event) {
        this.isDrawing = true;
        const rect = this.$refs.drawingCanvas.getBoundingClientRect();
        this.context.beginPath();
        this.context.moveTo(event.clientX - rect.left, event.clientY - rect.top);
      },
      draw(event) {
        if (!this.isDrawing) return;
        const rect = this.$refs.drawingCanvas.getBoundingClientRect();
        this.context.lineTo(event.clientX - rect.left, event.clientY - rect.top);
        this.context.strokeStyle = this.brushColor;
        this.context.lineWidth = this.brushSize;
        this.context.stroke();
      },
      stopDrawing() {
        this.isDrawing = false;
        this.context.closePath();
      },
      clearCanvas() {
        this.context.clearRect(0, 0, this.canvasWidth, this.canvasHeight);
      },
    },
  };
  </script>
  
  <style>
  .drawing-app {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    height: 100%;
  }
  
  .canvas-container {
    width: 80%; /* Adjust percentage as needed */
    height: 50vh; /* Responsive height */
    border: 1px solid #ccc;
    position: relative;
  }
  
  canvas {
    width: 100%; /* Responsive width */
    height: 100%; /* Responsive height */
    cursor: crosshair;
  }
  
  .controls {
    margin-top: 10px;
    display: flex;
    gap: 10px;
  }
  </style>
  