<script>
    import '../NewTaskFrom.css' 

    export default {
        data() {
            return {
                title: "",
                description: "",
                error: ""
            }
        },
        methods: {
            confirm() {
                if (!this.title.trim()) {
                    this.error = "⚠️ The task must have a title.";
                    return;
                }

                // Emitimos los datos al padre
                this.$emit("confirm-task", {
                    title: this.title,
                    description: this.description,
                    done: false
                });

                // Opcional: limpiar después
                this.title = "";
                this.description = "";
            },
            cancel() {
                this.$emit("cancel-task");
                this.title = "";
                this.description = "";
                this.error = "";
            }
        }
    }
</script>


<template>
    <div class="task-form-overlay">
        <div class="task-form">
            <h2>Creating a new task</h2>
            <input v-model="title" placeholder="Task title" />
            <p v-if="error" class="error-msg">{{ error }}</p>
            <textarea v-model="description" placeholder="Task description"></textarea>
            <div class="form-btns">
                <button @click="confirm">Confirm</button>
                <button @click="cancel">Cancel</button>
            </div>
        </div>
    </div>
</template>