<template>
    <div v-if="showError" class="alert text-red-500">
        {{ errorMessage }}
        <button @click="hideAlert">Cerrar</button>
    </div>
</template>
<script>
export default {
    name: "ErrorAvatar",
    props: {
        errorMessage: {
            type: String,
            default: 'Error'
        },
        showError: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        hideAlert() {
            this.$emit("changeShowError", !this.showError);
        }
    }
}
</script>