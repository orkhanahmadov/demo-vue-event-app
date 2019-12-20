<template>
    <div>
        <div v-for="(event, index) in events" :key="event.name" class="flex flex-wrap my-2">
            <div class="flex-1">{{ event.name }}</div>
            <div class="flex-1">{{ event.description }}</div>
            <div class="flex-1">{{ event.date }}</div>
            <div class="flex-1">{{ event.start_time + ' - ' + event.end_time }}</div>
            <div class="flex-1">
                <button type="button"
                        @click="fireDeleteEvent(index)"
                        class="bg-red-700 text-white px-2 py-1 text-sm rounded">Delete</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            events: {
                type: Array,
                required: true
            }
        },

        methods: {
            fireDeleteEvent(index) {
                this.$emit('delete-event', index)
            }
        }
    }
</script>