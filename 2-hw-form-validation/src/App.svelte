<script lang="ts">
  import RegisterForm from './components/RegisterForm.svelte'
  import ProfileForm from './components/ProfileForm.svelte'

  let isRegisterFormVisible = $state(true);
  const handleChangeFormBtnClick = () => {
    isRegisterFormVisible = !isRegisterFormVisible
  }
</script>

<main>
  <button class="toggle-form" onclick={handleChangeFormBtnClick}>
    {#if (isRegisterFormVisible)}
      Show profile form
    {:else}
      Show register form
    {/if}
  </button>
  <div class="card">
    {#if isRegisterFormVisible}
      <RegisterForm/>
    {:else}
      <ProfileForm/>
    {/if}
  </div>
</main>

<style>
  .toggle-form {
    background-color: #0093ff;
    color: white;
    line-height: 0.9;
  }
</style>
