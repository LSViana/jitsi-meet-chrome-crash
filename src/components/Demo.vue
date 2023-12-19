<template>
    <div class="root">
        <h1>Jitsi Meet Chrome Crash</h1>
        <p>This is a demo project to demonstrate Chromium browsers crashing when using the Jitsi Meet library.</p>
        <button @click="updateSlot">Update Slot</button>
        <div class="jitsi" ref="jitsi">
        </div>
    </div>
    <!-- This will be rendered in the shadow DOM of `.jitsi`. -->
    <div id="shadow-dom">
        <p>#1</p>
        <component is="slot" name="slot-1" />
        <p>#2</p>
        <component is="slot" name="slot-2" />
        <p>#3</p>
        <component is="slot" name="slot-3" />
        <p>#4</p>
    </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';

const jitsi = ref<HTMLElement>();
const api = ref<unknown>();
const slot = ref<1 | 2 | 3>(3);

onMounted(() => {
    const jitsiElement = jitsi.value
    const shadowDom = jitsiElement?.attachShadow({ mode: 'open' });

    shadowDom?.appendChild(document.querySelector('#shadow-dom')!);

    // @ts-ignore There are no type definitions for JitsiMeetExternalAPI.
    // Check documentation here: https://jitsi.github.io/handbook/docs/dev-guide/dev-guide-iframe.
    api.value = new JitsiMeetExternalAPI('meet.jit.si', {
        roomName: 'jitsi-meet-chrome-crash',
        width: 700,
        height: 700,
        parentNode: jitsiElement,
    });

    updateSlot();
});

function updateSlot(): void {
    // @ts-ignore There are no type definitions for JitsiMeetExternalAPI.
    const frame: HTMLIFrameElement = api.value?._frame;

    if (!frame) {
        throw Error('The iframe element isn\'t available.')
    }

    slot.value++;

    if (slot.value > 3) {
        slot.value = 1;
    }

    frame.slot = `slot-${slot.value}`;
}
</script>

<style lang="scss" scoped>
.root {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
}

.jitsi {
    margin-top: 1rem;
    background-color: rgba(255, 255, 255, 5%);
    border-radius: 0.25rem;
}
</style>