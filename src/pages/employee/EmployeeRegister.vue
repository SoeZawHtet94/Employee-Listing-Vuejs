
<template>
    <BreezeAuthenticatedLayout>
        <!-- component -->
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white">
                    <div class="overflow-x-auto border-x border-t">
                        <div
                            class="bg-teal-100 border-t-4 border-teal-500 rounded-b text-teal-900 px-4 py-3 shadow-md"
                            role="alert"
                            v-if="errors && errors.length">
                            <div class="flex" v-for="error of errors" :key="error">
                                <div class="py-1">
                                    <svg
                                        class="fill-current h-6 w-6 text-teal-500 mr-4"
                                        xmlns="http://www.w3.org/2000/svg"
                                        viewBox="0 0 20 20">
                                        <path
                                            d="M2.93 17.07A10 10 0 1 1 17.07 2.93 10 10 0 0 1 2.93 17.07zm12.73-1.41A8 8 0 1 0 4.34 4.34a8 8 0 0 0 11.32 11.32zM9 11V9h2v6H9v-4zm0-6h2v2H9V5z" />
                                    </svg>
                                </div>
                                <div>
                                    <p class="font-bold">
                                        {{ error }}
                                    </p>
                                </div>
                            </div>
                        </div>
                        <div class="w-full">
                            <form
                                @submit.prevent="saveEmployeeRegister"
                                class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                                <div class="mb-4">
                                    <label
                                        class="block text-gray-700 text-sm font-bold mb-2"
                                        for="username">
                                        Name
                                    </label>
                                    <input
                                        v-model="name"
                                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                        id="username"
                                        type="text"
                                        placeholder="Username" />
                                </div>
                                <div class="mb-4">
                                    <label
                                        class="block text-gray-700 text-sm font-bold mb-2"
                                        for="email">
                                        Email
                                    </label>
                                    <input
                                        v-model="email"
                                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                        id="email"
                                        type="text"
                                        placeholder="Email" />
                                </div>
                                <div class="mb-4">
                                    <label
                                        class="block text-gray-700 text-sm font-bold mb-2"
                                        for="dateofbirth">
                                        Date of Birth
                                    </label>
                                    <input
                                        v-model="dateofbirth"
                                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                        id="dateofbirth"
                                        type="Date"
                                        placeholder="Date of Birth" />
                                </div>
                                <div class="mb-4">
                                    <label
                                        class="block text-gray-700 text-sm font-bold mb-2"
                                        for="phno">
                                        Phone No
                                    </label>
                                    <input
                                        v-model="phno"
                                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                        id="phno"
                                        type="text"
                                        placeholder="Phone No" />
                                </div>
                                <div class="mb-4">
                                    <label
                                        class="block text-gray-700 text-sm font-bold mb-2"
                                        for="nrcno">
                                        NRC No
                                    </label>
                                    <input
                                        v-model="nrcno"
                                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                        id="nrcno"
                                        type="text"
                                        placeholder="NRC No" />
                                </div>
                                <div class="mb-4">
                                    <label
                                        class="block text-gray-700 text-sm font-bold mb-2"
                                        for="address">
                                        Address
                                    </label>
                                    <input
                                        v-model="address"
                                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                        id="address"
                                        type="text"
                                        placeholder="Address" />
                                </div>
                                <div class="mb-4">
                                    <label
                                        class="block text-gray-700 text-sm font-bold mb-2"
                                        for="gender">
                                        Gender
                                    </label>
                                    <select  v-model="gender"
                                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                        id="gender" >
                                        <option value="Male">Male</option>
                                        <option value="Female">Female</option>
                                    </select>
                                </div>
                                <div class="mb-4">
                                    <label
                                        class="block text-gray-700 text-sm font-bold mb-2"
                                        for="maritualstatus">
                                        Maritual Status
                                    </label>
                                    <select  v-model="maritualstatus"
                                        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                        id="maritualstatus" >
                                        <option value="Single">Single</option>
                                        <option value="Married">Married</option>
                                    </select>
                                </div>
                                <div class="flex items-center justify-between">
                                    <button
                                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                                        type="submit">
                                        Save New Employee
                                    </button>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>
<script>
import axios from '@/lib/axios'
import BreezeAuthenticatedLayout from '@/layouts/Authenticated.vue'

export default {
    data() {
        return {
            name: '',
            email: '',
            dateofbirth: '',
            phno: '',
            nrcno: '',
            address: '',
            gender: '',
            maritualstatus: '',
            errors: [],
        }
    },

    methods: {
        // Pushes posts to the server when called.
        saveEmployeeRegister() {
            axios
                .post(`api/employee-register`, {
                    name: this.name,
                    email: this.email,
                    phno: this.phno,
                    dateofbirth: this.dateofbirth,
                    nrcno: this.nrcno,
                    address: this.address,
                    gender: this.gender,
                    maritualstatus: this.maritualstatus,
                })
                .then(response => {
                    console.log(response.data);
                    if(response.data.status === 'OK'){
                        console.log("emp list");
                        this.$router.push({ path: '/employee-list' })
                    } else {
                        this.errors = [];
                        this.errors.push(response.data.message)
                    }
                   
                })
                .catch(e => {
                    this.errors.push(e)
                })
        },
    },
}
</script>
