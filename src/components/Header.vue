<template>
    <div>
        <h1>Bug and Quality Assurance Tracker</h1>
        <TicketForm @ticket-submit="addTicket" />
        <Tickets :tickets="tickets" :show-tickets="showTickets" 
        @delete-ticket="deleteTicket" 
        @mark-priority="markPriority"
         :priority="priority"  />
        </div>
</template>
<!-- :priority="priority" -->
<!-- @mark-priority="markPriority" -->
<!-- @toggle-priority="togglePriority" -->

<script>
import TicketForm from "./TicketForm.vue"
import Tickets from './Tickets.vue'

    export default {
        components: {
            Tickets,
            TicketForm
        },
        name: 'Header',
        data() {
            return {
                nextTicketId: 1,
                tickets: [],
                showTickets: false,
                priority: false,
                background: ''
            }
          },
        methods: {
            getNextTicketID() {
                return this.nextTicketId++;
            },
            addTicket(ticket) {
                ticket.id = this.getNextTicketID();
                this.tickets.push(ticket),
                this.showTickets = true;
            },
            deleteTicket(ticketId) {
                this.tickets = this.tickets.filter(ticket => ticket.id !== ticketId)
            },
            markPriority(ticketId) {
                this.ticket.priority = !this.ticket.priority
                console.log(this.tickets)
            }
              // togglePriority(ticketID) {
              //   ticket.priority = !ticket.priority
              // }
        }
    }

</script>



<style scoped>
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

  #container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    margin-top: 30px;
  }

  #formContainer {
    width: 750px;
    border: 1px solid black;
    border-radius: 10px;
    background-color: lightgray;
    padding: 10px;
  }

  .field{
    display: flex;
    margin-bottom: 10px;
  }

  label {
    width: 120px;
  }

  input, select {
    flex: 1;
    height: 25px;
  }

  button {
    margin-top: 10px;
  }

  h3 {
    margin-bottom: 5px;
  }

  #submitBtn {
    width: fit-content;
    display: flex;
    align-items: center;
    text-align: center;
    padding: 5px;
    margin-top: auto;
  }

  .priority {
    background-color: red;
  }


   
</style>