<template>
    <section class="section">
        <div id="app" class="container">
            <h1 class="title">Employees</h1>

            <employee-form @add:employee="addEmployee" />
            <employee-table
                :employees="employees"
                @delete:employee="deleteEmployee"
                @edit:employee="editEmployee"
            />
        </div>
    </section>
</template>

<script>
    import EmployeeTable from '@/components/EmployeeTable.vue';
    import EmployeeForm from '@/components/EmployeeForm.vue';

    export default {
        name: 'app',
        components: {
            EmployeeTable,
            EmployeeForm,
        },
        data() {
            return {
                employees: [
                    {
                        id: 1,
                        name: 'Richard Hendricks',
                        email: 'richard@piedpiper.com',
                    },
                    {
                        id: 2,
                        name: 'Bertram Gilfoyle',
                        email: 'gilfoyle@piedpier.com',
                    },
                    {
                        id: 3,
                        name: 'Dinesh Yugati',
                        email: 'dineshop@piedpiper.som'
                    },
                ],
            };
        },
        methods: {
            addEmployee(employee) {
                const lastId =
                    this.employees.length > 0
                         ? this.employees[this.employees.length - 1].id
                         : 0;
                const id = lastId + 1;
                const newEmployee = { ...employee, id };

                this.employees = [...this.employees, newEmployee];
            },
            deleteEmployee(id) {
                this.employees = this.employees.filter(employee => employee.id !== id);
            },
            editEmployee(id, updatedEmployee) {
                this.employees = this.employees.map(employee =>
                    employee.id === id ? updatedEmployee : employee
                );
            },
        },
    };
</script>

<style></style>
