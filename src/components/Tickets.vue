<template>
    <div v-if="showTickets">
        <div class="ticket-card" v-for="ticket in tickets" :key="ticket.id">
            <h4>{{ ticket.description }} </h4>
            <p class="ticket-info"><span>Description:</span> {{ ticket.importance }} </p>
            <p class="ticket-info"><span>Assigned To:</span> {{ ticket.assignedTo }} </p>
            <p class="ticket-info"><span>System:</span> {{ ticket.system }} </p>
            <p class="ticket-info"><span>Email:</span> {{ ticket.email }} </p>
            <div class="button-group">
                <button>Delete</button>
                <button>Mark as Priority</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            tickets: {
                type: Array,
                required: true
            },
            showTickets: {
                type: Boolean,
                required: true
            }
        }
    }

</script>

<style scoped>
.ticket-card {
    background-color: lightgray;
    border-radius: 5px;
    width: 350px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    margin: 10px auto;
    color: black;
    padding: 10px;
    line-height: 1.5;
}

.ticket-info {
    margin-bottom: 5px;
}

.button-group {
    margin-top: auto;
    display: flex;
    justify-content: flex-end;
}

.button-group button {
    margin-left: 10px;
    margin-top: 10px;
    width: 120px;
    text-align: center;
    padding: 5px;
}

span {
    font-weight: bold;
}




</style>