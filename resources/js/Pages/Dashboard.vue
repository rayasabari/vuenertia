<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/inertia-vue3';
import { ref } from '@vue/reactivity';

let counter = ref(0);

const increase = () => counter.value++;
const decrease = () => counter.value--;


</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Dashboard
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200 font-playfair">
                        You're logged in!

                        <button @click="increase" class="px-3 py-1 rounded-lg bg-emerald-400">+</button>
                        {{ counter }}
                        <button @click='decrease' class="px-3 py-1 rounded-lg bg-rose-600">-</button>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
