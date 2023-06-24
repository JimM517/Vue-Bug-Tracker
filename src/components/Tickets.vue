<template>
    <div>
        <li v-for="ticket in tickets" :key="ticket.id">
            {{ ticket.description }} - {{ ticket.importance }} - {{ ticket.assignedTo }} - {{ ticket.system }} - {{ ticket.email }}
        </li>
    </div>
</template>

<script>
    export default {
        props: {
            tickets: Array,
            required: true
        }
    }

</script>