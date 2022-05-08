<script setup>
import { useRoute } from 'vue-router'
import { useUsers } from '@/stores/user'
import { computed, ref } from 'vue'
import BreezeButton from '@/components/Button.vue'
import BreezeCheckbox from '@/components/Checkbox.vue'
import BreezeGuestLayout from '@/layouts/Guest.vue'
import BreezeInput from '@/components/Input.vue'
import BreezeLabel from '@/components/Label.vue'
import BreezeValidationErrors from '@/components/ValidationErrors.vue'

const route = useRoute()

const store = useUsers()

const form = ref({
    email: '',
    password: '',
    remember: false,
})

const processing = ref(false)

const setErrors = ref()

const errors = computed(() => setErrors.value)

const status = route.query.reset?.length > 0 ? atob(route.query.reset) : null

form.value = store.userLogin

const submitLogin = () => {
    store.login(setErrors, processing)
}
</script>

<template>
    <BreezeGuestLayout>
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
        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

        <BreezeValidationErrors class="mb-4" :errors="errors" />

        <form @submit.prevent="submitLogin">
            <div>
                <BreezeLabel for="email" value="Email" />
                <BreezeInput
                    id="email"
                    type="email"
                    class="mt-1 block w-full"
                    v-model="form.email"
                    required
                    autofocus
                    autocomplete="username" />
            </div>

            <div class="mt-4">
                <BreezeLabel for="password" value="Password" />
                <BreezeInput
                    id="password"
                    type="password"
                    class="mt-1 block w-full"
                    v-model="form.password"
                    required
                    autocomplete="current-password" />
            </div>

            <div class="block mt-4">
                <label class="flex items-center">
                    <BreezeCheckbox
                        name="remember"
                        :checked="form.remember"
                        v-model="form.remember" />
                    <span class="ml-2 text-sm text-gray-600">Remember me</span>
                </label>
            </div>

            <div class="flex items-center justify-end mt-4">
                <router-link
                    to="/forgot-password"
                    class="underline text-sm text-gray-600 hover:text-gray-900">
                    Forgot your password?
                </router-link>
                <BreezeButton class="ml-4" :processing="processing">
                    Login
                </BreezeButton>
            </div>
        </form>
    </BreezeGuestLayout>
</template>
