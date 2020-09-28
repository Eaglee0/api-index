<script>
    import {logindata} from './stores.js';
    let loginadatas;
    $: name = loginadatas.name;
    $: login = loginadatas.login;
    $: emaill = loginadatas.email;
    const data = logindata.subscribe(value => {
        loginadatas = value
    });
    function logout() {
        logindata.set({})
    }
</script>
{#if login == "yes"}
<h1>Hello {name}</h1>
<p>username: {name}</p>
<p>email: {emaill}</p>
{:else}
<p>Devi prima entrare: <a href="/login">Login</a></p>
{/if}
<br><a href="/">Home</a><br>
<button on:click={logout}>Esci</button>
