<script>
    import {logindata} from './stores.js';
    let loginadatas;
    $: name = loginadatas.name;
    $: login = loginadatas.login;
    const data = logindata.subscribe(value => {
        loginadatas = value
    });
</script>
<div>
    <h1>Home di algorithm-net.tk</h1>
    {#if login == "yes"}
    <a href="/users">User</a>
{:else}
<a href="/login">Login</a>

{/if}
</div>