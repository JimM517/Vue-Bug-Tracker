<template>
    <div>
        <h1>Bug and Quality Assurance Tracker</h1>
        <div id="container">
            <div id="formContainer">
                <h3>Submit a new issue:</h3>
                <form id="ticketForm" @submit.prevent="submitTicket()">
                    <div class="field">
                        <label for="description">Description:</label>
                        <input type="text" id="description" v-model="newIssue.description"/>
                    </div>
                    <div class="field">
                        <label for="importance">Importance:</label>
                        <select id="importance" v-model="newIssue.importance">
                            <option value=""> -- Select priority level -- </option>
                            <option value="low">Low</option>
                            <option value="medium">Medium</option>
                            <option value="high">High</option>
                            <option value="urgent">Urgent</option>
                        </select>
                    </div>
                    <div class="field">
                        <label for="assignedTo">Assigned To:</label>
                        <input type="text" id="assignedTo" v-model="newIssue.assignedTo"/>
                    </div>
                    <div class="field">
                        <label for="system">Operating System:</label>
                        <input type="text" id="system" v-model="newIssue.system"/>
                    </div>
                    <div class="field">
                        <label for="emailAddress">Email Address:</label>
                        <input type="text" id="emailAddress" v-model="newIssue.email"/>
                    </div>
                    <div class="field">
                        <button type="submit" id="submitBtn">Submit Issue</button>
                    </div>
                </form>
            </div>
        </div>

        <Tickets :tickets="tickets" :show-tickets="showTickets"/> 
        
    </div>
</template>


<script>
import Tickets from './Tickets.vue'

    export default {
        components: {
            Tickets
        },
        name: 'Header',
        data() {
            return {
                nextTicketId: 1,
                addTicket: '',
                tickets: [],
                newIssue: {
                    id: null,
                    description: '',
                    importance: '',
                    assignedTo: '',
                    system: '',
                    email: '',
                },
                showTickets: false
            }
        },
        methods: {
            getNextTicketID() {
                return this.nextTicketId++;
            },
            submitTicket() {
                const ticket = {
                    id: this.getNextTicketID(),
                    description: this.newIssue.description,
                    importance: this.newIssue.importance,
                    assignedTo: this.newIssue.assignedTo,
                    system: this.newIssue.system,
                    email: this.newIssue.email
                }

                this.tickets.push(ticket)

                this.newIssue = {
                    id: null,
                    description: '',
                    importance: '',
                    assignedTo: '',
                    system: '',
                    email: ''
                }
                this.showTickets = true;
                console.log(this.tickets)
            }
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


   
</style>