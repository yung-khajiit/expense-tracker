<template>
    <h3>Add A New Transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label form="text">Text</label>
            <input type="text" id="text" v-model="text" placeholder="Enter text...">
        </div>

        <div class="form-control">
            <label form="amount">amount (negative - expense, positive - income)</label>
            <input type="text" id="amount" v-model="amount" placeholder="Enter amount...">
        </div>
        <!-- {{ text }} - {{ amount }} -->
        <button class="btn">Add Transaction</button>
    </form>

</template>

<script setup>
    import {ref, defineEmits} from 'vue'
    const text = ref('')
    const amount = ref('')

    const emit = defineEmits([
        'transactionSubmitted'
    ])

    const onSubmit = () => {
        const transactionData = {
            text: text.value,
            amount: parseFloat(amount.value),
        }
        emit('transactionSubmitted', transactionData)

        text.value = ''
        amount.value = ''
    }

</script>