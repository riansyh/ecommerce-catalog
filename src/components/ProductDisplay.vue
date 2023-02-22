<script setup>
import './../assets/style/page.css'
import './../assets/style/rate.css'
import { onMounted, reactive } from 'vue';
import EmptyState from './EmptyState.vue'
import LoadingComponent from './LoadingComponent.vue'

const state = reactive({
    index: 1,
    isLoading: true,
    category: null,
    data: {},
});

async function fetchData() {
    state.isLoading = true;
    try {
        const response = await fetch(`https://fakestoreapi.com/products/${state.index}`);
        const data = await response.json();
        state.data = data;
        if (['women\'s clothing', 'men\'s clothing'].includes(state.data.category)) {
            state.category = state.data.category
        } else {
            state.category = null
        }
    } catch (error) {
        console.log(error);
    }
    state.isLoading = false;
}

function incrementCount() {
    if (state.index < 20) {
        state.index++;
    } else if (state.index === 20) {
        state.index = 1
    }
    fetchData()
}

onMounted(() => {
    fetchData();
})

</script>

<template>
    <main :class="state.category ? state.category === 'men\'s clothing' ? 'man' : 'woman' : 'empty'">
        <div class="background">
            <img src="/bg-pattern.svg" alt="image" />
        </div>

        <div class="product-card">
            <div class="product-card__image" v-if="!state.isLoading && state.category">
                <img :src="state.data.image" alt="image" />
            </div>
            <section class="product-card__detail" v-if="!state.isLoading && state.category">
                <div class="detail__header">
                    <h1 class="title">
                        {{ state.data.title ?? '' }}
                    </h1>
                    <div class="rate-container">
                        <h2 class="category">{{ state.data.category ?? '' }}</h2>
                        <div class="rate-item">
                            <p class="">{{ state.data.rating?.rate }}/5</p>
                            <div class="rate">
                                <div class="item" v-for="item in new Array(Math.round(state.data.rating.rate))" :key="item">
                                </div>
                                <div class="unfilled-item" v-for="item in new Array(5 - Math.round(state.data.rating.rate))"
                                    :key="item"></div>
                            </div>
                        </div>
                    </div>
                    <hr />
                    <p class="desc">
                        {{ state.data.description ?? '' }}
                    </p>
                </div>
                <div class="detail__footer">
                    <hr />
                    <p class="price">${{ state.data.price ?? '' }}</p>
                    <div class="btn-container">
                        <button class="button btn-primary">Buy now</button>
                        <button class="button btn-secondary" @click="incrementCount">Next product</button>
                    </div>
                </div>
            </section>

            <EmptyState @onNext="incrementCount" v-if="!state.isLoading && !state.category" />
            <LoadingComponent v-if="state.isLoading" />
        </div>
    </main>
</template>
