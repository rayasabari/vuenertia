<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head } from "@inertiajs/inertia-vue3";
import { ref, computed } from "@vue/reactivity";
import {
    Switch,
    Combobox,
    ComboboxInput,
    ComboboxOptions,
    ComboboxOption,
} from "@headlessui/vue";

let counter = ref(0);
let enabled = ref(false);

const people = [
    "Durward Reynolds",
    "Kenton Towne",
    "Therese Wunsch",
    "Benedict Kessler",
    "Katelyn Rohan",
];

const selectedPerson = ref(people[0]);
const query = ref("");

const filteredPeople = computed(() =>
    query.value === ""
        ? people
        : people.filter((person) => {
              return person.toLowerCase().includes(query.value.toLowerCase());
          })
);

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
                    <div
                        class="p-6 bg-white border-b border-gray-200 font-playfair"
                    >
                        You're logged in!

                        <button
                            @click="increase"
                            class="px-3 py-1 rounded-lg bg-emerald-400"
                        >
                            +
                        </button>
                        {{ counter }}
                        <button
                            @click="decrease"
                            class="px-3 py-1 rounded-lg bg-rose-600"
                        >
                            -
                        </button>
                        <Switch
                            v-model="enabled"
                            :class="enabled ? 'bg-blue-600' : 'bg-gray-200'"
                            class="relative inline-flex items-center h-6 rounded-full w-11"
                        >
                            <span class="sr-only">Enable notifications</span>
                            <span
                                :class="
                                    enabled ? 'translate-x-6' : 'translate-x-1'
                                "
                                class="inline-block w-4 h-4 transition transform bg-white rounded-full"
                            />
                        </Switch>
                        <Combobox v-model="selectedPerson">
                            <ComboboxInput
                            class="rounded-lg"
                                @change="query = $event.target.value"
                            />
                            <ComboboxOptions class="p-2 border rounded-lg">
                                <ComboboxOption
                                    v-for="person in filteredPeople"
                                    :key="person.id"
                                    :value="person"
                                    class="hover:bg-emerald-200"
                                >
                                    {{ person }}
                                </ComboboxOption>
                            </ComboboxOptions>
                        </Combobox>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
