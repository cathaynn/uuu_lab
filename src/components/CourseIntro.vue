<template>
    <li>
        <h2>{{ id }}-Current:{{ current }}-isCurrent:{{ isCurrent }}</h2>
        <button @click="toggleCourseDetail">show detail</button>
        <button @click="toggleCurrent">toggle isCurrent status</button>
        <ul v-if="detailsVisible">
            <li>{{ name }}</li>
            <li>{{ duration }}</li>
        </ul>
    </li>
</template>

<script>
export default {
    //emits:['toggle-current'],
    emits: {
        "toggle-current": function (id) {
            if (id) {
                return true
            } else {
                console.log("toggle-current should provide id, id missing!!")
                return false
            }
        }
    },
    props: {
        id: { type: String, required: true },
        name: { type: String, required: true },
        duration: {
            type: Number, required: true, validator: function (value) {
                return value > 7
            }
        },
        current: { type: Boolean, required: false, default: false }
    },
    data() {
        return {
            detailsVisible: true,
            isCurrent: this.current
        }
    },
    methods: {
        toggleCourseDetail() {
            this.detailsVisible = !this.detailsVisible
        },
        toggleCurrent() {
            // this.current = !this.current;
            // this.isCurrent = !this.isCurrent;
            this.$emit('toggle-current', this.id)
        }
    }
}
</script>