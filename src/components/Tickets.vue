<template>
    <div v-if="showTickets">
        <div class="ticket-card" v-for="ticket in tickets" :key="ticket.id" :class="priority ? 'priority' : 'ticket-card'">
            <div class="ticket-info">
                    <div>
                        <span>
                            TICKET:
                        </span>
                        {{ ticket.id }}
                    </div>
                    <div>
                        <span>Description:</span>
                        {{ ticket.description }}
                    </div>
                    <div>
                        <span>Assigned To:</span>
                        {{ ticket.assignedTo }}
                    </div>
                    <div>
                        <span>System:</span>
                        {{ ticket.system }}
                    </div>
                    <div>
                        <span>Email:</span>
                        {{ ticket.email }}
                    </div>
                    </div>
            <div class="button-group">
                <Button buttonText="Delete" @button-click="deleteTicket(ticket.id)" background=""  />
                <Button @button-click="markPriority(ticket.id)" :buttonText="ticket.priority ? 'Mark as Standard' : 'Mark as Priority'" background="" :priority="priority" />
                <!-- <Button buttonText="Mark as Priority" @button-click="togglePriority(ticket.id)" :buttonText="ticket.priority ? 'Mark as Standard' : 'Mark as Priority'" background="" /> -->


            </div>
        </div>
    </div>
</template>

<script>
import Button from '../components/Button.vue'

    export default {
        components: {
            Button
        },
        //REMINDER: PROPS ARE READ ONLY //
        props: {
            tickets: {
                type: Array,
                required: true
            },
            showTickets: {
                type: Boolean,
                required: true
            },
            priority: {
                type: Boolean,
                required: true
            },
        },
        methods: {
            deleteTicket(ticketId) {
                this.$emit('delete-ticket', ticketId)
            },
            markPriority(ticketId) {
                this.$emit('mark-priority', ticketId);
            },
         
        }
    }

</script>

<style scoped>
.ticket-card {
    background-color: #f2f2f2;
    border: 1px solid black;
    border-radius: 5px;
    width: 650px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
    margin: 10px auto;
    color: black;
    padding: 10px;
    line-height: 1.5;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    /* width: 650px;
    border: 1px solid black;
    border-radius: 10px;
    background-color: lightgray;
    padding: 10px;
    margin: 10px auto; */
}

.ticket-info {
    /* margin: 2px;
    line-height: 1rem; */
    margin-bottom: 5px;
    display: flex;
    flex-direction: column;
}

.ticket-info div {
    display: flex;
    align-items: center;
}

.ticket-info span {
    font-weight: bold;
    width: 120px;
}

.ticket-info div span {
    margin-right: 5px;
}

.ticket-card h4 {
    font-size: 18px;
    font-weight: bold;
}

/* .ticket-info span {
    font-weight: bold;
} */

.button-group {
    margin-top: auto;
    display: flex;
    justify-content: flex-end;
    transition: background-color 0.3s, transform 0.3s;
    align-self: flex-end;
}

.button-group button {
    margin-left: 10px;
    margin-top: 0px;
    width: 120px;
    text-align: center;
    padding: 5px;
}

.button-group button:hover {
    background-color: #e6e6e6;
    transform: scale(1.05);
}

span {
    font-weight: bold;
}

.delete {
    background-color: red;
}

.priority {
    background-color: yellow;
}




</style>