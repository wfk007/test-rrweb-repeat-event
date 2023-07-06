<template>
    <div>
        <button @click="onStart">onStart</button>
        <button @click="onStop">onStop</button>
        <button @click="onToggle">toggle-iframe</button>
        <iframe v-if="showIframe"></iframe>
        <video controls width="250">
            <source src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.webm" type="video/webm" />
            <source src="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4" type="video/mp4" />
            Download the
            <a href="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.webm">WEBM</a>
            or
            <a href="https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4">MP4</a>
            video.
        </video>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { record } from 'rrweb';

let stopRecordFn;
const events = [];
const showIframe = ref(false);

const onStart = () => {
    stopRecordFn = record({
        sampling: {
            mousemove: false,
            mouseInteraction: false,
        },
        slimDOMOptions: true,
        emit(event) {
            events.push(event);
        },
    });
};
const onStop = () => {
    stopRecordFn();
    console.log(events);
};

const onToggle = () => {
    showIframe.value = !showIframe.value;
};
</script>
