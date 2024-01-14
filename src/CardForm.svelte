<!-- CardForm.svelte -->
<script lang="ts">
  import { onMount } from "svelte";
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  let cardData: {cardholder:string; cardNumber: string; expiryMounth: string; expiryYear: string; cvv: string } = {
    cardholder: '',
    cardNumber: '',
    expiryMounth: '',
    expiryYear: '',
    cvv: '',
  };

  function formatСardholder(value: string): string {
    // Format card number with a space after every four digits
    const sanitizedValue = value.replace(/^[A-Za-z\s]+$/, '');
    return sanitizedValue();
  }

  function formatCardNumber(value: string): string {
    // Format card number with a space after every four digits
    const sanitizedValue = value.replace(/[^0-9]/g, ''); // Remove non-numeric characters
    const formattedValue = sanitizedValue.replace(/(\d{4})/g, '$1 ');
    return formattedValue.trim();
  }

  function formatExpiryDate(value: number): number {
    // Format expiry date as MM/YY
    const sanitizedValue = value.replace(/[^0-9]/g, ''); // Remove non-numeric characters
    
    return sanitizedValue;
  }

  function formatExpiryMounth(value: string): string {
    // Format expiry date as MM/YY
    const sanitizedValue = value.replace(/[^0-9]/g, ''); // Remove non-numeric characters
    if (number > 12) number = 12;
    return sanitizedValue;
  }

  function cvv(value: string): string {
    // Format expiry date as MM/YY
    const sanitizedValue = value.replace(/[^0-9]/g, ''); // Remove non-numeric characters
    const formattedValue = sanitizedValue.replace(/(\d{4})/g, '$1 ');
    return formattedValue.trim();
  }

  function validateSurname(value: string): boolean {
    const regex = /^[A-Za-z\s]+$/;
    return regex.test(value);
  }

  function handleSubmit() {
    // Validate fields before submitting
    if (
      cardData.cardNumber.trim() === '' ||
      cardData.expiryDate.trim() === '' ||
      cardData.cvv.trim() === '' ||
      cardData.surname.trim() === ''
    ) {
      alert('Please fill in all fields before submitting.');
      return;
    }

    // Additional validation for specific fields (e.g., surname)
    if (!validateSurname(cardData.surname)) {
      alert('Invalid characters in the surname field. Please use only letters and spaces.');
      return;
    }

    // if (cardData.expiryMounth.replace(/\s/g, '').length > 12) {
    //   alert('Maximum allowed entries for card number is 12.');
    //   return;
    // }

    // Handle form submission logic here
    console.log('Submitted data:', cardData);
    // You can send this data to a server or perform other actions as needed
  }
  
</script>

<style>
  /* Add any necessary styles */
  @import './CardForm.css';
</style>


<form on:submit|preventDefault={handleSubmit}>
  <div class="credit-card">
  <label for="cardholder">Cardholder name:</label>
  <input
    type="text"
    id="cardholder"
    bind:value={cardData.cardholder}
    on:input={() => cardData.cardholder = formatСardholder(cardData.cardholder)}
    placeholder="e.g. Jane Appleseed"
    maxlength="50"
  />

  <br><label for="cardNumber">Card Number:</label>
  <input
    type="text"
    id="cardNumber"
    bind:value={cardData.cardNumber}
    on:input={() => cardData.cardNumber = formatCardNumber(cardData.cardNumber)}
    placeholder="Enter card number"
    maxlength="19"
  />

  <br><label for="expiryMounth">Expiry Mounth:</label>
  <input
    type="number"
    id="expiryDate"
    bind:value={cardData.expiryMounth}
    on:input={() => cardData.expiryMounth = formatExpiryMounth(cardData.expiryMounth)}
    max="12"
    min="01"
    placeholder="MM"
    maxlength="2"
    
  />

  <br><label for="expiryMounth">Expiry Date:</label>
  <input
    type="number"
    id="expiryDate"
    bind:value={cardData.expiryYear}
    on:input={() => cardData.expiryYear}
    placeholder="YY"
    min="00"
    maxlength="2"
  />

  <br><label for="cvv">CVV:</label>
  <input
    type="password"
    id="cvv"
    bind:value={cardData.cvv}
    on:input={() => cardData.cvv = cvv(cardData.cvv)}
    placeholder="Enter CVV"
    maxlength="3"
  />

  <!-- <button type="submit">Confirm</button> -->
  <button type="button" on:click={handleSubmit}>Confirm</button>
</div>
</form>

<div class="cardform">
<p>{cardData.cardNumber || '0000 0000 0000 0000'}</p>
<p>{cardData.cardholder || 'Name Surname'}</p>

<p>Exp. date {cardData.expiryMounth || '00'}/{cardData.expiryYear || '00'}</p>
</div>
