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
      if (target.value.length < 2 ) {
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

  // Валидация поля password
  const handlePasswordInputChange = (e: Event) => {
    const target = e.target as HTMLInputElement;

    if (target) {
      // Проверка на длину строки
      if (target.value.length < 8 ) {
        if (!formData.password.errors.includes("Password must be at least 8 characters")){
          formData.password.errors.push("Password must be at least 8 characters");
        }
      } else {
        formData.password.errors = formData.password.errors.filter((error) => error !== "Password must be at least 8 characters");
      }

      // Проверка на отсутствие любых символов кроме букв
      const onlyLettersAndNumbersRegExp = /^(?=.*[a-zA-Z])(?=.*\d).+$/;

      if (!onlyLettersAndNumbersRegExp.test(target.value)) {
        if(!formData.password.errors.includes("Username must have at least one letter and one digit")) {
          formData.password.errors.push("Username must have at least one letter and one digit");
        }
      } else {
        formData.password.errors = formData.password.errors.filter((error) => error !== "Username must have at least one letter and one digit");
      }

      // Установка/снятие флага валидации
      formData.password.isValidating = formData.password.errors.length === 0;
    }
  };

  // Валидация поля confirmPassword
  const handleConfirmPasswordInputChange = (e: Event) => {
    const target = e.target as HTMLInputElement;
    console.log("target.value", target.value)
    console.log("formData.password.value", formData.password.value)
    formData.confirmPassword.isValidating = target.value === formData.password.value;
    console.log("formData.confirmPassword.isValidating", formData.confirmPassword.isValidating)

    if(!formData.confirmPassword.isValidating) {
      if (!formData.confirmPassword.errors.includes("Passwords do not match")) {
        formData.confirmPassword.errors.push("Passwords do not match");
      }
    } else {
      formData.confirmPassword.errors = formData.confirmPassword.errors.filter((error) => error !== "Passwords do not match");
    }
  };

  const handleFormSubmit = (e: SubmitEvent) => {
    e.preventDefault();
    console.log("form submitted");
  };
</script>

<h3>Register</h3>
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
      onfocus={() => {formData.username.touched = true}}
    />
    {#if (formData.username.errors.length > 0)}
      <span class="error-message">{formData.username.errors.join(", ")}</span>
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
      type="password"
      id="password"
      bind:value={password.value}
      oninput={e => handlePasswordInputChange(e)}
      onfocus={() => formData.password.touched = true}
    />
    {#if (formData.password.errors.length > 0)}
      <span class="error-message">{formData.password.errors.join(", ")}</span>
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
      bind:value={confirmPassword.value}
      oninput={e => handleConfirmPasswordInputChange(e)}
      onfocus={() => {
        formData.confirmPassword.touched = true;
        formData.confirmPassword.value = "";
      }}
    />
    {#if (formData.confirmPassword.errors.length > 0)}
      <span class="error-message">{formData.confirmPassword.errors.join(", ")}</span>
    {/if}
  </div>

  <input type="submit" value="Submit">
</form>

<style>
  h3 {
    text-align: center;
  }

  form {
    min-width: 450px;
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
