<template>
    <div id="employee-form">
        <form @submit.prevent="handleSubmit">
            <div class="field">
                <label for="name" class="label">Employee name</label>
                <input
                    ref="first"
                    type="text"
                    class="input"
                    :class="{ 'is-danger': submitting && invalidName }"
                    id="name"
                    v-model="employee.name"
                    @focus="clearStatus"
                    @keypress="clearStatus"
                >
            </div>
            <div class="field">
                <label for="email" class="label">Employee email</label>
                <input
                    type="text"
                    class="input"
                    :class="{ 'is-danger': submitting && invalidEmail }"
                    id="email"
                    v-model="employee.email"
                    @focus="clearStatus"
                    @keypress="clearStatus"
                >
            </div>
            <div class="field">
                <div v-if="error && submitting" class="notification is-danger">
                    Please fill out all the required fields
                </div>
                <div v-if="success" class="notification is-success">
                    Employee successfully added
                </div>
            </div>
            <div class="field">
                <button class="button is-primary">Add Employee</button>
            </div>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'employee-form',
        data() {
            return {
                submitting: false,
                error: false,
                success: false,
                employee: {
                    name: '',
                    email: '',
                },
            };
        },
        computed: {
            invalidName() {
                return this.employee.name === '';
            },
            invalidEmail() {
                return this.employee.email === '';
            },
        },
        methods: {
            handleSubmit() {
                this.submitting = true;
                this.clearStatus();

                if (this.invalidName || this.invalidEmail) {
                    this.error = true;
                    return;
                }

                this.$emit('add:employee', this.employee);
                this.$refs.first.focus();

                this.employee = {
                    name: '',
                    email: '',
                };

                this.error = false;
                this.success = true;
                this.submitting = false;
            },
            clearStatus() {
                this.success = false;
                this.error = false;
            },
        },
    };
</script>

<style scoped></style>
