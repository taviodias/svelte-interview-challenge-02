<script>
  import {login} from './utils';

  let email = '';
  let password = '';
  let error = '';

  $: buttonDisabled = email === '' || password.length < 6;

  const onClick = async () => {
    error = '';
    buttonDisabled = true;
    try{
      await login({email, password});
      alert('Login Successfull!');
      email = '';
      password = '';
    }catch(e){
      error = e.message;
    }
    buttonDisabled = false;
  }
</script>

<div class='wrapper'>
  <div class='login-form'>
    <h1>Login Form 🐞</h1>
    <!-- Coloque a mensagem de erro de login na div abaixo. Mostre a div somente se houver uma mensagem de erro. -->
    {#if error}
      <div class='errorMessage'>{error}</div>
    {/if}
    <div class='row'>
      <label for='email'>Email</label>
      <input id='email' type='email' autocomplete='off' bind:value={email} />
    </div>
    <div class='row'>
      <label for='password'>Password</label>
      <input id='password' type='password' bind:value={password} />
    </div>
    <div class='button'>
      <button on:click={onClick} disabled={buttonDisabled}>Login</button>
    </div>
  </div>
</div>
