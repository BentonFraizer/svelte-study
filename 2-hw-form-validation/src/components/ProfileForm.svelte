<script lang="ts">
  // ProfileForm

  import type { FormField } from "../lib/types";

  interface ProfileFormState {
    username: FormField;
    password: FormField;
    confirmPassword: FormField;
    fullName: FormField;
    age: FormField;
    bio: FormField;
    email: FormField;
    phone: FormField;
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

  let formData: ProfileFormState = $derived({ username, password, confirmPassword, fullName, age, bio, email, phone })
  $inspect("bio: ", bio)
  let formValidationMessage = $state("")

  // Валидация поля username
  const handleUsernameInputOnblur = (e: Event) => {
    const target = e.target as HTMLInputElement;
    formValidationMessage = "";

    if (target) {
      // Проверка на длину строки
      if (target.value.length < 2) {
        if (!formData.username.errors.includes("Username must be at least 2 characters")) {
          formData.username.errors.push("Username must be at least 2 characters");
        }
      } else {
        formData.username.errors = formData.username.errors.filter((error) => error !== "Username must be at least 2 characters");
      }

      // Проверка на отсутствие любых символов кроме букв
      const onlyLettersRegExp = /^[a-zA-Z]+$/;

      if (!onlyLettersRegExp.test(target.value)) {
        if (!formData.username.errors.includes("Username must have letter only")) {
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
  const handlePasswordInputOnblur = (e: Event) => {
    const target = e.target as HTMLInputElement;
    formValidationMessage = "";

    if (target) {
      // Проверка на длину строки
      if (target.value.length < 8) {
        if (!formData.password.errors.includes("Password must be at least 8 characters")) {
          formData.password.errors.push("Password must be at least 8 characters");
        }
      } else {
        formData.password.errors = formData.password.errors.filter((error) => error !== "Password must be at least 8 characters");
      }

      // Проверка на отсутствие любых символов кроме букв
      const onlyLettersAndNumbersRegExp = /^(?=.*[a-zA-Z])(?=.*\d).+$/;

      if (!onlyLettersAndNumbersRegExp.test(target.value)) {
        if (!formData.password.errors.includes("Username must have at least one letter and one digit")) {
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
  const handleConfirmPasswordInputOnblur = (e: Event) => {
    const target = e.target as HTMLInputElement;
    formValidationMessage = "";
    formData.confirmPassword.isValidating = target.value === formData.password.value;

    if (!formData.confirmPassword.isValidating) {
      if (!formData.confirmPassword.errors.includes("Passwords do not match")) {
        formData.confirmPassword.errors.push("Passwords do not match");
      }
    } else {
      formData.confirmPassword.errors = formData.confirmPassword.errors.filter((error) => error !== "Passwords do not match");
    }
  };

  // Валидация поля Full Name
  const handleFullNameInputOnblur = (e: Event) => {
    const target = e.target as HTMLInputElement;

    // 1. Два слова, разделенные одним пробелом
    if (!/^\S+ \S+$/.test(target.value)) {
      if (!formData.fullName.errors.includes("Input must contain exactly two words separated by a single space.")) {
        formData.fullName.errors.push("Input must contain exactly two words separated by a single space.");
      }
    } else {
      formData.fullName.errors = formData.fullName.errors.filter((error) => error !== "Input must contain exactly two words separated by a single space.");
    }

    // 2. Только буквы латинского алфавита
    if (!/^[A-Za-z ]+$/.test(target.value)) {
      if (!formData.fullName.errors.includes("Input must contain only Latin letters.")) {
        formData.fullName.errors.push("Input must contain only Latin letters.");
      }
    } else {
      formData.fullName.errors = formData.fullName.errors.filter((error) => error !== "Input must contain only Latin letters.");
    }

    // 3. Каждое слово должно начинаться с большой буквы
    if (!/^[A-Z][a-z]* [A-Z][a-z]*$/.test(target.value)) {
      if (!formData.fullName.errors.includes("Each word must start with a capital letter.")) {
        formData.fullName.errors.push("Each word must start with a capital letter.");
      }
    } else {
      formData.fullName.errors = formData.fullName.errors.filter((error) => error !== "Each word must start with a capital letter.");
    }

    // Установка/снятие флага валидации
    formData.fullName.isValidating = formData.fullName.errors.length === 0;
  }

  // Обработчик события для поля age. Запрет ввода любых символов кроме чисел, включая точки и запятые
  const handleAgeInputChange = (e: Event) => {
    const target = e.target as HTMLInputElement;
    formData.age.value = target.value.replace(/\D/g, '');
  }

  // Валидация поля age
  const handleAgeInputOnblur = (e: Event) => {
    const target = e.target as HTMLInputElement;
    if (Number(target.value) < 18 || Number(target.value) > 100) {
      if (!formData.age.errors.includes("Age must be between 18 and 100.")) {
        formData.age.errors.push("Age must be between 18 and 100.");
      }
    } else {
      formData.age.errors = formData.age.errors.filter((error) => error !== "Age must be between 18 and 100.");
    }

    // Установка/снятие флага валидации
    formData.age.isValidating = formData.age.errors.length === 0;
  }

  // Валидация поля bio
  const handleBioInputOnblur = (e: Event) => {
    const target = e.target as HTMLInputElement;

    if (target.value.length < 10 || target.value.length > 200) {
      if (!formData.bio.errors.includes("Text should contain from 10 to 200 symbols.")) {
        formData.bio.errors.push("Text should contain from 10 to 200 symbols.");
      }
    } else {
      formData.bio.errors = formData.bio.errors.filter((error) => error !== "Text should contain from 10 to 200 symbols.");
    }

    // Установка/снятие флага валидации
    formData.bio.isValidating = formData.bio.errors.length === 0;
  }

  // Валидация поля email
  const handleEmailInputOnblur = (e: Event) => {
    const target = e.target as HTMLInputElement;

    if(!/^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+.[A-Za-z]{2,}$/.test(target.value)) {
      if (!formData.email.errors.includes("Invalid email address.")) {
        formData.email.errors.push("Invalid email address.");
      }
    } else {
      formData.email.errors = formData.email.errors.filter((error) => error !== "Invalid email address.");
    }

    // Установка/снятие флага валидации
    formData.email.isValidating = formData.email.errors.length === 0;
  }

  const handleFormSubmit = (e: Event) => {
    e.preventDefault();
    // console.log("e: ", e)
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
      onblur={(e) => {
        handleUsernameInputOnblur(e);
        formData.username.touched = true
      }}
    />
    {#if (formData.username.errors.length > 0)}
      <div class="error-message">{formData.username.errors[0]}</div>
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
    <!-- тип text в поле password оставлен специально для удобства разработки и тестирования -->
    <input
      type="text"
      id="password"
      name="password"
      bind:value={password.value}
      onblur={(e) => {
        handlePasswordInputOnblur(e);
        formData.password.touched = true
      }}
    />
    {#if (formData.password.errors.length > 0)}
      <div class="error-message">{formData.password.errors[0]}</div>
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
      onblur={(e) => {
        handleConfirmPasswordInputOnblur(e)
        formData.confirmPassword.touched = true;
      }}
      onfocus={() => formData.confirmPassword.value = ""}
    />
    {#if (formData.confirmPassword.errors.length > 0)}
      <div class="error-message">{formData.confirmPassword.errors[0]}</div>
    {:else}
      <div class="empty"></div>
    {/if}
  </div>

  <hr/>

  <div>
    <label
      for="fullName"
      class:not-valid={formData.fullName.touched && !formData.fullName.isValidating}
    >
      Full Name:
    </label>
    <input
      type="text"
      id="fullName"
      name="fullName"
      bind:value={fullName.value}
      onblur={(e) => {
        handleFullNameInputOnblur(e)
        formData.fullName.touched = true
      }}
    />
    {#if (formData.fullName.errors.length > 0)}
      <div class="error-message">{formData.fullName.errors[0]}</div>
    {:else}
      <div class="empty"></div>
    {/if}
  </div>
  <div>
    <label for="age" class:not-valid={formData.age.touched && !formData.age.isValidating}>Age:</label>
    <input
      type="text"
      id="age"
      name="age"
      bind:value={age.value}
      oninput={handleAgeInputChange}
      onblur={(e) => {
        handleAgeInputOnblur(e)
        formData.age.touched = true
      }}
    />
    {#if (formData.age.errors.length > 0)}
      <div class="error-message">{formData.age.errors[0]}</div>
    {:else}
      <div class="empty"></div>
    {/if}
  </div>
  <div>
    <label for="bio" class:not-valid={formData.bio.touched && !formData.bio.isValidating}>Bio:</label>
    <textarea
      id="bio"
      name="bio"
      rows="5"
      cols="50"
      bind:value={bio.value}
      onblur={(e) => {
        handleBioInputOnblur(e)
        formData.bio.touched = true
      }}
    ></textarea>
    {#if (formData.bio.errors.length > 0)}
      <div class="error-message">{formData.bio.errors[0]}</div>
    {:else}
      <div class="empty"></div>
    {/if}
  </div>
  <div>
    <label for="email" class:not-valid={formData.email.touched && !formData.email.isValidating}>Email:</label>
    <input
      type="email"
      id="email"
      name="email"
      bind:value={email.value}
      onblur={(e) => {
        handleEmailInputOnblur(e)
        formData.email.touched = true
      }}
    />
    {#if (formData.email.errors.length > 0)}
      <div class="error-message">{formData.email.errors[0]}</div>
    {:else}
      <div class="empty"></div>
    {/if}
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
