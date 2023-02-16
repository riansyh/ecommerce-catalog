<template>
    <div class="empty-state">
        <p>This product is unavailable to show</p>
        <button class="button btn-black" @click="next">Next product</button>
</div>
</template>

<script>
export default {
    name: "EmptyState",

    methods: {
        next() {
            this.$emit('onNext')
        }
    }
}
</script>
