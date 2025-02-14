<template>
  <div class="tickets">
    <div class="form">
      <h2>Get Your Ticket Now!</h2>
      <p>Join us for the Best Event of the Year!</p>
      <div class="form-i">
        <input type="text" placeholder="Full Name" v-model="fullName" required />
        <input type="text" placeholder="NIC Number" v-model="nicNumber" required />
        <select name="batch" id="batch" v-model="batch">
          <option value="BTDT">Batch 1</option>
          <option value="BE">Batch 2</option>
          <option value="EE">Batch 3</option>
          <option value="CS">Batch 4</option>
        </select>
        <input type="phone" placeholder="Contact number" v-model="contactNumber" required />
        <div v-if="isloading" class="loading">
            <span></span>
            <span></span>
            <span></span>
            <span></span>
            <span></span>
          </div>
          <span style="color: brown;">{{ formError }}</span>
          <p style="text-align: center; text-wrap: wrap;">{{ successMessage }}</p>
        <button @click="register">Get Tickets</button>
        
      </div>
    </div>
    <div class="content">
      <div class="title">
        <h2>Payment Information</h2>

        <p>
          Thank you for choosing to celebrate Holi with us! To
          secure your ticket, please complete your payment by [Date/Time]. We
          offer convenient payment options through bank transfer. Kindly refer
          to the details below to make your payment.
        </p>
      </div>

      <div class="bank-details">
        <h3>Bank Details</h3>
        <p>
          <strong>Bank:</strong> <span>{{ bankDetails.bank }}</span><br />
          <strong>Account Name:</strong>
          <span>{{ bankDetails.accountName }}</span><br />
          <strong>Account Number:</strong> <span>{{ bankDetails.accountNumber }}</span
          ><br />
          <strong>Branch:</strong> <span>{{ bankDetails.branch }}</span><br />
        </p>
      </div>

      <div class="contact">
        <p>
          Once you have made the transfer, please send us a confirmation message
          with the transaction details (reference number, screenshot of the
          transfer, etc.) to <br>
          <a :href="`mailto:${contact.email}`">Email</a>
          <br> or 
          <span v-for="phone in contact.phone" :key="phone">
            <br>
            <a style="margin-left: 0.5rem;" :href="`https://wa.me/${phone.number}`">{{ phone.name }}</a>
          </span> 
          <br>on Whatsapp, so we can confirm your booking.
        </p>

        <p>
          For any inquiries or further assistance regarding payments, please
          don't hesitate to contact us at the numbers provided.
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tickets",
  data() {
    return {
      bankDetails: {
        bank: "Bank Name",
        accountName: "Your Account Name or Event Name",
        accountNumber: "Your Account Number",
        branch: "Branch Name or Location",
      },
      contact: {
        email: "unkounnumber@gmail.com",
        phone: [ 
          {
            name: "user1",
            number: "+94771234567",
          },
          {
            name: "user2",
            number: "+94771234567",
          },
          {
            name: "user3",
            number: "+94771234567",
          },
          {
            name: "user4",
            number: "+94771234567",
          },
        ],
      },
      formError: null,
      fullName: null,
      nicNumber: null,
      batch: null,
      contactNumber: null,
      isloading: false,
      successMessage: null,
    };
  },
  methods: {
    register() {
      // Validate the form
      if (!this.fullName || !this.nicNumber || !this.batch || !this.contactNumber) {
        this.formError = "Please fill all the fields";
        return;
      }
      // Validate full name to only contain letters
      if (!/^[a-zA-Z ]+$/.test(this.fullName)) {
        this.formError = "Please enter a valid name";
        return;
      }
      // Validate NIC number to only contain numbers and letters
      if (!/^[0-9a-zA-Z]+$/.test(this.nicNumber) || this.nicNumber.length < 10) {
        this.formError = "Please enter a valid NIC number";
        return;
      }

      // Validate contact number to only contain numbers
      if (!/^[0-9]+$/.test(this.contactNumber)) {
        this.formError = "Please enter a valid contact number";
        return;
      }
      this.isloading = true;
      fetch(`https://script.google.com/macros/s/AKfycbw66DsowpHZNi0V6jlN43h98Ozs01vL58O8Qu1meM2xLLi2_6hmK2xQ-8IdIanvJTy0/exec?name=${this.fullName}&nic=${this.nicNumber}&batch=${this.batch}&contact=${this.contactNumber}`, {
        method: "GET",
      })
        .then(response => response.json())
        .then(data => {
          if (data.status === 101){
            this.formError = "You have already registered for the event";
            this.isloading = false;
            return;
          } else if (data.status === 200){
            
            this.successMessage = "You have successfully registered for the event. Please pay the registration fee and send us the transaction details to get your tickets";
            this.isloading = false;
            return;
          } else {
            this.formError = "An error occurred while registering for the event";
            this.isloading = false;
            return;
          }
        })
        .catch(error => {
          console.error("Error:", error);
          this.formError = "An error occurred while registering for the event";
          this.isloading = false;
        });

    },
  },
};
</script>

<style lang="css" scoped>
* {
  animation: appear 2s;
  animation-timeline: view();
  animation-range: entry 0% cover 40%;
}
.tickets {
  display: grid;
  grid-template-areas: "form content";
  justify-content: space-around;
  align-items: center;
  margin: 3rem 0;
}

.form {
  height: 100%;
  grid-area: form;
  padding: 2rem;
  background-color: rgba(255, 255, 255, 0.425);
  backdrop-filter: blur(50%);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}
.form h2 {
    font-size: clamp(1.5rem, 2.5vw, 2rem);
  margin-bottom: 0.5rem;
  color: #06195c;
}
.form p {
  color: #06195c;
}
.form-i {
  margin: 1rem 0;
  display: grid;
  gap: 1rem;
}
input {
  background-color: transparent;
  border-bottom: 2px solid #06195c;
  padding: 1rem;
  border-top: none;
  border-left: none;
  border-right: none;
  color: #06195c;
}
input:focus {
  outline: none;
  color: #e1615b;
}
select {
  padding: 1rem;
  border: none;
  background-color: transparent;
  border-bottom: 2px solid #06195c;
  color: #06195c;
}
select:focus {
  outline: none;
  color: #e1615b;
}
option {
  background-color: transparent;
  border-radius: 5px;
  border: none;
  color: #06195c;
}
button {
  margin-top: 1rem;
  padding: 1rem;
  font-weight: 700;
  font-size: 1rem;
  border-radius: 20px;
  border: none;
  background-color: #06195c;
  color: white;
  cursor: pointer;
}
button:hover {
  background-color: #e1615b;
}
.content {
  display: grid;
  grid-template-areas:
    "title title title"
    "contact contact bank-details"
    "contact contact bank-details";
  max-width: 500px;
  grid-area: content;
  padding: 2rem;
  background-color: rgba(255, 255, 255, 0.425);
  backdrop-filter: blur(50%);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}
.title {
  grid-area: title;
  color: #06195c;
}
.title h2 {
    font-size: clamp(1.5rem, 2.5vw, 2rem);
  margin-bottom: 0.5rem;
}
.bank-details {
  width: 220px;
  margin-left: 1rem;
  grid-area: bank-details;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #06195c;
}
.bank-details h3 {
  margin-bottom: 0.5rem;
}
.bank-details p {
  display: grid;
  gap: 0;
}
.contact {
  grid-area: contact;
  color: #06195c;
  margin-top: 1rem;
}
.contact p {
  margin-bottom: 1rem;
}

@media (max-width: 768px) {
  .tickets {
    grid-template-areas:
      "form"
      "content";
    gap: 2rem;
  }
  .content {
    grid-template-areas:
      "title"
      "bank-details"
      "contact";
    max-width: 100%;
  }
  .title {
    font-size: clamp(1.5rem, 2.5vw, 2rem);
    text-align: center;
    margin-bottom: 1rem;
  }
  .bank-details {
    margin-top: 1rem;
  }
  .bank-details p {
    font-size: clamp(1rem, 2.5vw, 1.25rem);
    display: grid;
    gap: 0.5rem;
  }
  .bank-details h3 {
    margin-bottom: 0.5rem;
  }
  .contact {
    margin-top: 1rem;
  }
  p {
    font-size: clamp(1rem, 2.5vw, 1.25rem);
  }
  .contact p {
    font-size: clamp(1rem, 2.5vw, 1.25rem);
    margin-bottom: 1rem;
  }
}
.loading {
  --speed-of-animation: 0.9s;
  --gap: 6px;
  --first-color: #4c86f9;
  --second-color: #49a84c;
  --third-color: #f6bb02;
  --fourth-color: #f6bb02;
  --fifth-color: #2196f3;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100px;
  gap: 6px;
  height: 100px;
}

.loading span {
  width: 4px;
  height: 50px;
  background: var(--first-color);
  animation: scale var(--speed-of-animation) ease-in-out infinite;
}

.loading span:nth-child(2) {
  background: var(--second-color);
  animation-delay: -0.8s;
}

.loading span:nth-child(3) {
  background: var(--third-color);
  animation-delay: -0.7s;
}

.loading span:nth-child(4) {
  background: var(--fourth-color);
  animation-delay: -0.6s;
}

.loading span:nth-child(5) {
  background: var(--fifth-color);
  animation-delay: -0.5s;
}

@keyframes scale {
  0%,
  40%,
  100% {
    transform: scaleY(0.05);
  }

  20% {
    transform: scaleY(1);
  }
}
@keyframes appear {
  from {
    opacity: 0;
    scale: 0.5;
  }
  to {
    opacity: 1;
    scale: 1;
  }
}
</style>
