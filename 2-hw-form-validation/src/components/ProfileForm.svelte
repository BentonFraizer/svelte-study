<script lang="ts">
  // ProfileForm

  import type { FormField } from "../lib/types";

  interface ProfileFormState {
    username: FormField;
    password: FormField;
    confirmPassword: FormField;
  }

  let username = $state({
    value: "",
    errors: [],
    isValidating: false,
    touched: false,
  });

  let password = $state({
    value: "",
    errors: [],
    isValidating: false,
    touched: false,
  });

  let confirmPassword = $state({
    value: "",
    errors: [],
    isValidating: false,
    touched: false,
  });

  let fullName = $state({
    value: "",
    errors: [],
    isValidating: false,
    touched: false,
  });

  let age = $state({
    value: "",
    errors: [],
    isValidating: false,
    touched: false,
  });

  let bio = $state({
    value: "",
    errors: [],
    isValidating: false,
    touched: false,
  });

  let email = $state({
    value: "",
    errors: [],
    isValidating: false,
    touched: false,
  });

  let phone = $state({
    value: "",
    errors: [],
    isValidating: false,
    touched: false,
  });

  let formData: ProfileFormState = $derived({ username, password, confirmPassword, fullName, age, bio, email, phone });
  $inspect("fullName: ", formData)

  const handleFormSubmit = (e: Event) => {
    e.preventDefault();
    console.log("e: ", e)
  };

</script>

<h3>Profile</h3>
<form onsubmit={handleFormSubmit}>
  <div>
    <label
      for="username"
      class:not-valid={formData.username.touched && !formData.username.isValidating}
    >
      Username:
    </label>
    <input
      type="text"
      id="username"
      name="username"
      bind:value={username.value}
      onfocus={() => {formData.username.touched = true}}
    />
    {#if (formData.username.errors.length > 0)}
      <div class="error-message">{formData.username.errors.join(", ")}</div>
    {:else}
      <div class="empty"></div>
    {/if}
  </div>

  <div>
    <label
      for="password"
      class:not-valid={formData.password.touched && !formData.password.isValidating}
    >
      Password:
    </label>
    <input
      type="text"
      id="password"
      name="password"
      bind:value={password.value}
      onfocus={() => formData.password.touched = true}
    />
    {#if (formData.password.errors.length > 0)}
      <div class="error-message">{formData.password.errors.join(", ")}</div>
    {:else}
      <div class="empty"></div>
    {/if}
  </div>

  <div>
    <label
      for="confirmPassword"
      class:not-valid={formData.confirmPassword.touched && !formData.confirmPassword.isValidating}
    >
      Confirm password:
    </label>
    <input
      type="password"
      id="confirmPassword"
      name="confirmPassword"
      bind:value={confirmPassword.value}
      onfocus={() => {
        formData.confirmPassword.touched = true;
        formData.confirmPassword.value = "";
      }}
    />
    {#if (formData.confirmPassword.errors.length > 0)}
      <div class="error-message">{formData.confirmPassword.errors.join(", ")}</div>
    {:else}
      <div class="empty"></div>
    {/if}
  </div>

  <hr/>

  <div>
    <label for="fullName">Full Name:</label>
    <input
      type="text"
      id="fullName"
      name="fullName"
      bind:value={fullName.value}
    />
  </div>
  <div>
    <label for="age">Age:</label>
    <input
      type="number"
      id="age"
      name="age"
      bind:value={age.value}
    />
  </div>
  <div>
    <label for="bio">Bio:</label>
    <textarea id="bio" name="bio" rows="5" cols="50" bind:value={bio.value}></textarea>
  </div>
  <div>
    <label for="email">Email:</label>
    <input
      type="email"
      id="email"
      name="email"
      bind:value={email.value}
    />
  </div>
  <div>
    <label for="phone">Phone:</label>
    <input
      type="text"
      id="phone"
      name="phone"
      bind:value={phone.value}
    />
  </div>

  <input type="submit" value="Submit">
</form>

<style>
  div {
    text-align: right;
  }

  .error-message {
    height: 17px;
    margin: 0;
    text-align: right;
    display: block;
    font-size: 11px;
    color: red;
  }

  .not-valid {
    color: red;
  }

  .empty {
    margin: 0;
    height: 17px;
  }

  hr {
    width: 100%;
    border: 1px solid rebeccapurple;
  }

  textarea {
    resize: none;
  }
</style>
