<script lang="ts">
  interface FormField {
    value: string;
    touched: boolean;
    errors: string[];
    isValidating: boolean;
  }

  interface FormState {
    username: FormField;
    password: FormField;
    confirmPassword: FormField;
  }

  let username = $state("");
  let password = $state("");
  let confirmPassword = $state("");

  let formData: FormState = $state({
    username: {
      value: username,
      errors: [],
      isValidating: false,
      touched: false,
    },
    password: {
      value: password,
      errors: [],
      isValidating: false,
      touched: false,
    },
    confirmPassword: {
      value: confirmPassword,
      errors: [],
      isValidating: false,
      touched: false,
    },
  })

  const handleUsernameInputChange = (e: Event) => {
    const target = e.target as HTMLInputElement;
    if (target) {
      const onlyLettersMoreThanTwoRegExp = /^[a-zA-Z]{2,}$/;
      formData.username.isValidating = onlyLettersMoreThanTwoRegExp.test(target.value);

    }
  };

  // const handleUsernameInputFocus = () => {
  //   console.log("username field in focus");
  // }

  const handleFormSubmit = (e: SubmitEvent) => {
    e.preventDefault();
    console.log("form submitted");
  };

  // $inspect("formData: ", formData);
  // $inspect("password: ", password);
  // $inspect("confirmPassword: ", confirmPassword);
</script>

<form onsubmit={e => handleFormSubmit(e)}>
  <p>
    <label for="username" class:not-valid={formData.username.touched && !formData.username.isValidating}>Username:</label>
    <input
      type="text"
      id="username"
      bind:value={username}
      oninput={e => handleUsernameInputChange(e)}
      onfocus={() => formData.username.touched = true}
    />
  </p>
  <p>
    <!-- todo в конце решения задания можно заменить типы с type="text" на type="password" -->
    <label for="password">Password:</label>
    <input type="text" id="password" bind:value={password}/>
  </p>
  <p>
    <label for="confirmPassword">Confirm password:</label>
    <input type="text" id="confirmPassword" bind:value={confirmPassword}/>
  </p>
  <input type="submit" value="Submit">
</form>

<style>
  form {
    border: 5px solid gray;
    border-radius: 40px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-end;
    padding: 50px;
  }

  .not-valid {
    color: red;
  }
</style>

