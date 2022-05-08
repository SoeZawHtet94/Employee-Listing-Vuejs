<script setup>
import BreezeAuthenticatedLayout from '@/layouts/Authenticated.vue'
</script>

<template>
    <BreezeAuthenticatedLayout>
    
          <div class="max-w-2xl mx-auto bg-white p-10">
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Employee Detail Information
            </h2>
        </div>
        <div class="max-w-2xl mx-auto bg-white p-16">

            <form>
            <div class="grid gap-6 mb-6 lg:grid-cols-2">
                <div>
                    <label for="first_name" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Name</label>
                    <input type="text" id="first_name" :value="employee.name" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" disabled>
                </div>
                <div>
                    <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Email</label>
                    <input type="text" id="email" :value="employee.email" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Doe" disabled>
                </div>
                <div>
                    <label for="dateofbirth" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Date of Birth</label>
                    <input type="text" id="dateofbirth" :value="employee.date_of_birth" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="Flowbite" disabled>
                </div>  
                <div>
                    <label for="phone" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Phone number</label>
                    <input type="tel" id="phone" :value="employee.phone_no" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="123-45-678" pattern="[0-9]{3}-[0-9]{2}-[0-9]{3}" disabled>
                </div>
                <div>
                    <label for="gender" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Gender</label>
                    <input type="text" id="gender" :value="employee.gender"  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="flowbite.com" disabled>
                </div>
                <div>
                    <label for="maritual_status" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Maritual Status</label>
                    <input type="text" id="maritual_status" :value="employee.maritual_status"  class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="" disabled>
                </div>
                 <div>
                    <label for="address" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Address</label>
                    <input type="text" id="address" :value="employee.address" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="" disabled>
                </div>
            </div>

        </form>
    </div>
    </BreezeAuthenticatedLayout>
</template>
<script>
import axios from '@/lib/axios'
export default {
    data() {
        return {
            employee: {},
            errors: [],
        }
    },

    // Fetches posts when the component is created.
    created() {
        axios
            .get(`/api/employee/` + this.$route.params.id)
            .then(response => {
                if (response.data.status === 'OK') {
                    console.log(response.data.employee)
                    this.employee = response.data.employee
                } else {
                    this.errors.push('No Data Found')
                }
            })
            .catch(e => {
                this.errors.push(e)
            })
    },
}
</script>
