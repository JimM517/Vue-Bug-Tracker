<template>
    <div>
        <h1>Bug and Quality Assurance Tracker</h1>
        <ticket-form @ticket-submit="addTicket" />
        <tickets :tickets="tickets" :show-tickets="showTickets" 
        @delete-ticket="deleteTicket" 
        @mark-priority="markPriority"
        :priority="priority"
         />
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
                background: '',
                updateLocalStorage: () => {
            localStorage.setItem('tickets', JSON.stringify(this.tickets))
        }
            }
          },
        methods: {
            getNextTicketID() {
                return this.nextTicketId++;
            },
            addTicket(ticket) {
                ticket.id = this.getNextTicketID();
                ticket.priority = false;
                this.tickets.push(ticket),
                this.showTickets = true;
                //updating local storage
                this.updateLocalStorage();
            },
            deleteTicket(ticketId) {
                this.tickets = this.tickets.filter(ticket => ticket.id !== ticketId)
                this.updateLocalStorage()
            },
            markPriority(ticketId) {
                // ticket.priority = ticket.priority
                // console.log(this.tickets)
                const ticket = this.tickets.find(ticket => ticket.id === ticketId);
                if (ticket) {
                    ticket.priority = !ticket.priority
                }
                this.$forceUpdate()
            },
        
              // togglePriority(ticketID) {
              //   ticket.priority = !ticket.priority
              // }
        },
        // checking for exisiting data in local storage array and loading it into tickets array
        created() {
          const storedTickets = localStorage.getItem('tickets');
          if (storedTickets) {
            this.tickets = JSON.parse(storedTickets);
            this.showTickets = true;
          }
        },
        watch: {
          tickets: {
            handler() {
              this.updateLocalStorage()
            },
            deep: true
          }
        },
      
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