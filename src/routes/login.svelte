<script>
  import {logindata} from './stores.js';
  let name_s;
  let email_s;
  let password_s;
  let email_l;
  let password_l;
  let name_res = "";
  let loginadatas;
    $: name = loginadatas.name;
    $: loginyes = loginadatas.login;
    const data = logindata.subscribe(value => {
        loginadatas = value
    });

  function onlogin() {
    console.log(email_l, password_l);
    let userdata = {
      email: email_l,
      password: password_l,
    };
    name_res = "Caricamento..."
    console.log(JSON.stringify(userdata));
    fetch("http://algorithm-net.tk/loginapi/api/login", {
      method: "POST",
      body: JSON.stringify(userdata),
    })
      .then(function (response) {
        response.json().then(function (data) {
          console.log(data);
          name_res = "Benvenuto " + data.name;
          logindata.set(data);
        });
      })
      .catch(function (error) {
        console.log("Fetch error");
      });
  }
  function onsignup() {
    console.log(name_s, email_s, password_s);
    let userdata = {
      name: name_s,
      email: email_s,
      password: password_s,
    };
    console.log(JSON.stringify(userdata));
    fetch("http://algorithm-net.tk/loginapi/api/signup", {
      method: "POST",
      credentials: "include",
      body: JSON.stringify(userdata),
    })
      .then(function (response) {
        response.json().then(function (data) {
          console.log(data);
        });
      })
      .catch(function (error) {
        console.log("Fetch error");
      });
  }
</script>


<a href="/">Home</a>
{#if loginyes == "yes"}
<a href="/users">User</a>
<p>Utente: {name}</p>

{:else}
<p>esegui l'accesso</p>
{/if}
<div id="login">
  <h2>Login</h2>
  <label for="password">Email</label>
  <input
    type="text"
    id="email_l"
    bind:value={email_l}
    placeholder="your email" />
  <label for="password">Password</label>
  <input
    type="text"
    id="password_l"
    bind:value={password_l}
    placeholder="Your password" />

  <button id="submit" on:click={onlogin}>Submit message</button><br />
  <h2>{name_res}</h2>
</div><br />

<div id="signup">
  <h2>Signup</h2>
  <label for="Name">Name</label>
  <input type="text" id="name_s" bind:value={name_s} placeholder="Your name" />
  <label for="email">Email</label>
  <input
    type="text"
    id="email_s"
    bind:value={email_s}
    placeholder="your email" />
  <label for="password">Password</label>
  <input
    type="text"
    id="password_s"
    bind:value={password_s}
    placeholder="Your password" />

  <button on:click={onsignup} id="submit">Submit message</button>
</div>
