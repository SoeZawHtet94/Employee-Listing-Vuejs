<script setup>
import { useUsers } from '@/stores/user'

const store = useUsers()

const auth = store.authUser
</script>

<template>
    <div
        class="relative navbar-light flex items-top justify-center min-h-screen bg-gray-100 dark:bg-gray-900 sm:items-center sm:pt-0">
        <div class=" navbar-light ">
            <div class="hidden fixed top-0 right-0 px-6 py-4 sm:block">
                <router-link
                    v-if="auth"
                    to="/dashboard"
                    class="text-sm text-gray-700 underline">
                    Dashboard
                </router-link>

                <template v-else>
                    <router-link
                        to="/login"
                        class="ml-4 text-sm text-gray-700 underline">
                        Log in
                    </router-link>
                    <router-link
                        to="/register"
                        class="ml-4 text-sm text-gray-700 underline">
                        Register
                    </router-link>
                </template>
            </div>
        </div>
        

        <div class="py-4 bg-black text-white">
        <div class="container mx-auto flex flex-col md:flex-row my-12 md:my-36">
            <div class="flex flex-col w-full lg:w-2/5 p-8">
                <p class="text-3xl md:text-5xl text-yellow-500 my-4 leading-relaxed md:leading-snug">Wellcome</p>
          
            </div>
            <div class=" flex flex-col lg:w-3/5 justify-center w-full lg:-mt-12">
                <div class="container">
                <div class="relative flex flex-col min-w-0 break-words w-full">
                    <div class="flex-auto p-5 lg:p-10">
                    <img src="https://user-images.githubusercontent.com/54521023/152731049-cc744a56-1d6f-4945-9566-0fa3b7ad1d24.png" alt="contact image">
                    </div>
                </div>
                </div>
            </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.navbar-light{
    background-color: #2d444f;
    box-shadow: 0px 14px 80px rgba(34, 35, 58, 0.2);

  }

.bg-gray-100 {
    background-color: #f7fafc;
    background-color: rgba(247, 250, 252, var(--tw-bg-opacity));
}

.border-gray-200 {
    border-color: #edf2f7;
    border-color: rgba(237, 242, 247, var(--tw-border-opacity));
}

.text-gray-400 {
    color: #cbd5e0;
    color: rgba(203, 213, 224, var(--tw-text-opacity));
}

.text-gray-500 {
    color: #a0aec0;
    color: rgba(160, 174, 192, var(--tw-text-opacity));
}

.text-gray-600 {
    color: #718096;
    color: rgba(113, 128, 150, var(--tw-text-opacity));
}

.text-gray-700 {
    color: #4a5568;
    color: rgba(74, 85, 104, var(--tw-text-opacity));
}

.text-gray-900 {
    color: #1a202c;
    color: rgba(26, 32, 44, var(--tw-text-opacity));
}

@media (prefers-color-scheme: dark) {
    .dark\:bg-gray-800 {
        background-color: #2d3748;
        background-color: rgba(45, 55, 72, var(--tw-bg-opacity));
    }

    .dark\:bg-gray-900 {
        background-color: #1a202c;
        background-color: rgba(26, 32, 44, var(--tw-bg-opacity));
    }

    .dark\:border-gray-700 {
        border-color: #4a5568;
        border-color: rgba(74, 85, 104, var(--tw-border-opacity));
    }

    .dark\:text-white {
        color: #fff;
        color: rgba(255, 255, 255, var(--tw-text-opacity));
    }

    .dark\:text-gray-400 {
        color: #cbd5e0;
        color: rgba(203, 213, 224, var(--tw-text-opacity));
    }
}
</style>
