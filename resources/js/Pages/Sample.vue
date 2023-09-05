<template>
        <form @submit.prevent="submit">
            <input
                :value="this.form.name"
                @input="this.form.name = $event.target.value"
                @change="submit"
            >
            <p>
                {{ this.form.errors.name }}
            </p>
        </form>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { useForm } from "laravel-precognition-vue-inertia";

export default defineComponent({
    name: 'Sample',
    props: {
        name: {
            type: String,
            required: true,
        },
    },
    data() {
        return {
            form: useForm("post" ,"/sample", {
                name: "",
            })
        }
    },
    methods: {
        submit() {
            this.form.transform( () => {
                return {
                    name: "this is validate",
                }
            }).validate('name')
            this.form.transform( () => {
                return {
                    name: "this is submit",
                }
            }).submit();
        }
    }
})
</script>
