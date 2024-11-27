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

  let formData: FormState = $derived({ username, password, confirmPassword })

  // Валидация поля username
  const handleUsernameInputChange = (e: Event) => {
    const target = e.target as HTMLInputElement;

    if (target) {
      // Проверка на длину строки
      if (target.value.length <= 1 ) {
        if (!formData.username.errors.includes("Username must be at least 2 characters")){
          formData.username.errors.push("Username must be at least 2 characters");
        }
      } else {
        formData.username.errors = formData.username.errors.filter((error) => error !== "Username must be at least 2 characters");
      }

      // Проверка на отсутствие любых символов кроме букв
      const onlyLettersRegExp = /^[a-zA-Z]+$/;

      if (!onlyLettersRegExp.test(target.value)) {
        if(!formData.username.errors.includes("Username must have letter only")) {
          formData.username.errors.push("Username must have letter only");
        }
      } else {
        formData.username.errors = formData.username.errors.filter((error) => error !== "Username must have letter only");
      }

      // Установка/снятие флага валидации
      formData.username.isValidating = formData.username.errors.length === 0;
    }
  };

  const handleFormSubmit = (e: SubmitEvent) => {
    e.preventDefault();
    console.log("form submitted");
  };

  // $inspect("formData: ", formData);
  // $inspect("password: ", password);
  // $inspect("confirmPassword: ", confirmPassword);
</script>

<form onsubmit={e => handleFormSubmit(e)}>
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
      bind:value={username.value}
      oninput={e => handleUsernameInputChange(e)}
      onfocus={() => formData.username.touched = true}
    />
    {#if (formData.username.errors.length > 0)}
      <span class="error-message">{formData.username.errors.join(", ")}</span>
    {/if}
  </div>

  <div>
    <!-- todo в конце решения задания можно заменить типы с type="text" на type="password" -->
    <label for="password">Password:</label>
    <input type="text" id="password" bind:value={password.value}/>
  </div>
  <div>
    <label for="confirmPassword">Confirm password:</label>
    <input type="text" id="confirmPassword" bind:value={confirmPassword.value}/>
  </div>
  <input type="submit" value="Submit">
</form>

<style>
  form {
    min-width: 400px;
    border: 5px solid gray;
    border-radius: 40px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-end;
    padding: 50px;
  }

  div {
    margin-bottom: 20px;
    text-align: right;
  }

  .error-message {
    text-align: right;
    display: block;
    font-size: 11px;
    color: red;
  }

  .not-valid {
    color: red;
  }
</style>
