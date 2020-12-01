<template>
    <div id="employee-form">
        <form @submit.prevent="handleSubmit">
            <label for="">Employee Name</label>
            
            <input 
            type="text"
            class="{'has-error' : submitting && invalidName }"
            v-model="employee.name" 
            @focus="clearStatus"
            @keypress="clearStatus"
            >
            
            <label for="">Employee Email</label>
            
            <input 
            type="text"
            class="{'has-error' : submitting && invalidName }"
            v-model="employee.email"
            @focus="clearStatus"
            >

            <p v-if="error && submitting" class="error-message">Please fill in the required fields correctly!</p>
            <p v-if="success && submitting" class="success-message">Employee Successfully added!</p>
            
            <button>Add Employees</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'employee-form',
    data(){
        return {
            submitting: false,
            error: false,
            success: false,
            employee: {
                name: '',
                email: '',
            },
        }
    },
    methods: {
        handleSubmit(){

            this.submitting = true;
            this.clearStatus()

            if(this.invalidName || this.invalidEmail){
                this.error = true;
                return
            }

            this.$emit('add:employee', this.employee)

            this.employee = {
                name: '',
                email: '',
            }
            this.error = false
            this.success = true
            this.submitting = false
        },

        clearStatus(){
            this.success = false
            this.error = false
        }
    },
    computed: {

        invalidName(){
            return this.employee.name === ''
        },

        invalidEmail(){
            return this.employee.email === ''
        }
    }
}
</script>

<style scoped>

form{
    margin-bottom: 2rem;
}

[class*='-message']{
    font-weight: 500;
}

.error-message {
    color: #d33c40;
}

.success-message{
    color: green;
}
</style>