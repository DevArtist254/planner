<template>
    <div class="project" :class="{ complete: project.complete }">
        <div class="actions" @click="toggleDetails">
            <h3>{{ project.title }}</h3>
        </div>
        <div class="icon">
            <span class="material-symbols-outlined" @click="toggleComplete">
                done_all
            </span>
            <span class="material-symbols-outlined">
                edit
            </span>
            <span class="material-icons-outlined" @click="deleteProject">
                delete
            </span>
        </div>
        <div class="details" v-show="tD">
            <p>{{ project.details }}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "SingleProject",
    props: ['project'],
    data() {
        return {
            tD: false,
            url: "http://localhost:3000/projects/" + this.project.id
        }
    },
    methods: {
        toggleDetails() {
            this.tD = !this.tD
        },
        deleteProject() {
            fetch(this.url, { method: 'DELETE' })
                .then(() => this.$emit('delete', this.project.id))
        },
        toggleComplete() {
            fetch(this.url, {
                method: 'PATCH',
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ complete: this.project.complete })
            }).then(() => this.$emit('updateComplete', this.project.id))
        }
    }
}
</script>

<style>
.project {
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
    border-left: 4px solid #e90074;
}

h3 {
    cursor: pointer;
}

.action {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.project.complete {
    border-left: 4px solid #00ce89;
}
</style>