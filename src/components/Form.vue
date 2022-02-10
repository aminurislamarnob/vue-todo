<template>
    <form @submit.prevent="$emit('submitTodo')">
        <input type="text" placeholder="Type and hit enter..." class="composer__input mb-4" :class="{'field__error' : isError}" :value="modelValue" @keydown="$emit('update:modelValue', $event.target.value)"  />
    </form>
</template>

<script>
export default {
    props: {
        modelValue:{
            type: String,
            requred: true
        },
        isError:{
            type: Boolean
        }
    }
}
</script>