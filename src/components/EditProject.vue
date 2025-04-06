<template>
    <form @submit.prevent="handleSubmit">
        <label>Title</label>
        <input type="text" v-model="title" required>
        <label>Details</label>
        <textarea v-model="details" required></textarea>
        <button>Add Project</button>
    </form>
</template>

<script>
export default {
    name: "EditProject",
    props: ['id'],
    data() {
        return {
            title: '',
            details: '',
            uri: `http://localhost:3000/projects/${this.id}`
        }
    },
    methods: {
        handleSubmit() {
            const updatedProject = {
                title: this.title,
                details: this.details,
            }

            fetch(this.uri, {
                method: 'PATCH',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(updatedProject)
            }).then(() => this.$router.push('/'));
        }
    },
    mounted() {
        fetch(this.uri).then(res => res.json()).then(
            (data) => {
                this.title = data.title
                this.details = data.details
            }
        )
    }
}
</script>

<style></style>