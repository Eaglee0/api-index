<script>
  import { onMount } from "svelte";
  import { listen } from "svelte/internal";
  import { logindata } from "./stores.js";
  import { apisdata } from "./stores.js";
  let loginadatas;
  let listapis;
  $: member1 = listapis.apis_list[0].name;
  $: link1 = listapis.apis_list[0].link;
  $: member2 = listapis.apis_list[1].name;
  $: link2 = listapis.apis_list[1].link;
  $: name = loginadatas.name;
  $: login = loginadatas.login;
  const data = logindata.subscribe((value) => {
    loginadatas = value;
  });
  const data2 = apisdata.subscribe((value) => {
    listapis = value;
  })
  

  onMount(() => {
    fetch("http://algorithm-net.tk/timeapi/listapis").then(response => response.json()).then(data=>apisdata.set(
      {"apis_list":
      [
        {"name": data.apis_list[0].name,"link": data.apis_list[0].link},
        {"name": data.apis_list[1].name,"link": data.apis_list[1].link}
      ],
       "get":true
      }
      
      ))
    
  });
</script>

<div>
  <h1>Home di algorithm-net.tk</h1>
  {#if login == 'yes'}
    <a href="/users">User</a>
  {:else}<a href="/login">Login</a>{/if}
</div>
<div>
  {#if listapis.get == true}
    <ul>
      <li>{member1}, <a href={link1}>link</a></li>
      <li>{member2}, <a href={link2}>link</a></li>
    </ul>
    {:else}
    <h3>Caricamento...</h3>
  {/if}
</div>
