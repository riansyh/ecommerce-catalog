<script setup>
import { defineEmits } from 'vue'

const emit = defineEmits(['onNext'])

function next() {
    emit('onNext')
}

</script>

<template>
    <div class="empty-state">
        <p>This product is unavailable to show</p>
        <button class="button btn-black" @click="next">Next product</button>
    </div>
</template>


