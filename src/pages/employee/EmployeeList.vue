<script setup>
import BreezeAuthenticatedLayout from '@/layouts/Authenticated.vue'
</script>

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
                        <table
                            class="table-auto w-full"
                            v-if="employeeData && employeeData.length">
                            <thead class="border-b">
                                <tr class="bg-gray-100">
                                    <th class="text-left p-4 font-medium">
                                        Name
                                    </th>
                                    <th class="text-left p-4 font-medium">
                                        Email
                                    </th>
                                    <th class="text-left p-4 font-medium">
                                        Phone
                                    </th>
                                    <th class="text-left p-4 font-medium">
                                        Address
                                    </th>
                                    <th class="text-left p-4 font-medium">
                                        Action
                                    </th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr
                                    class="border-b hover:bg-gray-50"
                                    v-for="employee of employeeData" :key="employee">
                                    <td class="p-4">{{ employee.name }}</td>
                                    <td class="p-4">{{ employee.email }}</td>
                                    <td class="p-4">{{ employee.phone_no }}</td>
                                    <td class="p-4">{{ employee.address }}</td>
                                    <td class="p-4"> 
                                        <a :href="`/employee/${employee.id}`" id="edit" class="edit">Edit</a>
                                        <a :href="`/employee/${employee.id}`" id="detail"  class="detail">Detail</a>
                                        <a @click="empdelete(employee.id)" href="" id="delete"  class="delete">delete</a>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </BreezeAuthenticatedLayout>
</template>
<script>
import axios from '@/lib/axios'

export default {
    data() {
        return {
            employeeData: [],
            errors: [],
        }
    },

    // Fetches posts when the component is created.
    created() {
        axios
            .get(`/api/employee-list`)
            .then(response => {
                if (response.data.status === 'OK') {
                    this.employeeData = response.data.employee
                } else {
                    this.errors.push('No Data Found')
                }
            })
            .catch(e => {
                this.errors.push(e)
            })
    },

    methods: {
        // Pushes posts to the server when called.
        empdelete(employeeid) {
            console.log(employeeid)
            axios
                .delete(`/api/employee-delete/` + employeeid)
                .then(response => {
                    if(response.data.status === 'OK'){
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

<style >
.delete {
  color:#f11313;
}
.detail {
  color:#392cf0;
}
.edit {
  color:#0ae745;
}
</style>
