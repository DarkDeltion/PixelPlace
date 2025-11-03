<template>
    <nav class="tool-bar">
        <Toolbar
            v-for="tool in tools"
            :key="tool.label"
            :label="tool.label"
        >
            <img :src="tool.src" :alt="tool.label" class="tool-icon" />
        </Toolbar>
    </nav>

    <CanvasDesktop />

    <Sidebar />
</template>

<script setup>
import Toolbar from '../components/canvas/desktop/toolbar.vue'
import Sidebar from '../components/canvas/desktop/sidebar.vue'
import CanvasDesktop from '../components/canvas/desktop/canvas.vue'
// list of tools and their icon paths (icons should live in public/ToolIcons)
const tools = [
    { label: 'Bucket', src: '/ToolIcons/bucket%20tool.png' },
    { label: 'Circle', src: '/ToolIcons/circle%20tool.png' },
    { label: 'Color Picker', src: '/ToolIcons/color%20picker.png' },
    { label: 'Drawing', src: '/ToolIcons/drawing-tool.png' },
    { label: 'Eraser', src: '/ToolIcons/eraser.png' },
    { label: 'Grid', src: '/ToolIcons/grid%20tool.png' },
    { label: 'Line', src: '/ToolIcons/line%20tool.png' },
    { label: 'Square', src: '/ToolIcons/square%20tool.png' },
    { label: 'Undo', src: '/ToolIcons/undo.png' },
    { label: 'Redo', src: '/ToolIcons/redo.png' },
]

</script>

<style scoped>
    .tool-bar {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 10px;
        height: 100px;
        background: #1e1e1e;
        padding: 0 20px;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        z-index: 40; /* above canvas and sidebar */
        box-shadow: 0 2px 10px rgba(0,0,0,0.2);
    }

</style>