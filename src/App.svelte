<script>
  import { countries } from "./data";
  let country = "";
  let number = "";
  $: phone = country + number;
  const regex = /^\+(?:[0-9] ?){6,14}[0-9]$/;
  $: invalid = !regex.test(phone);

  function handleSubmit(e) {
    alert(`You entered ${phone}`);
  }
</script>

<style>
  .message {
    margin: 1em 0;
    font-size: 1rem;
    font-style: italic;
  }

  .invalid {
    color: hsl(0, 100%, 33%);
  }
</style>

<form on:submit|preventDefault={handleSubmit}>
  <fieldset>
    <legend>Phone number</legend>
    <label htmlFor="country-code">Country</label>
    <input
      bind:value={country}
      placeholder="+44"
      type="text"
      list="countrycodes"
      id="country-code"
      aria-invalid={invalid} />
    <datalist id="countrycodes">
      {#each countries as country}
        <option key={country.code} value={`+${country.phone}`}>
          {country.label} (+{country.phone})
        </option>
      {/each}
    </datalist>
    <label htmlFor="number">Number</label>
    <input
      bind:value={number}
      id="number"
      type="phone"
      placeholder="12345678"
      aria-invalid={invalid} />
    <div class:invalid class="message">
      {invalid ? 'Invalid phone number' : ''}
    </div>
    <input type="submit" value="Submit" disabled={invalid} />
  </fieldset>
</form>
