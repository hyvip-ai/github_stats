<script>
  import { scale } from "svelte/transition";
  
  export let repo = {}
</script>

<div transition:scale>
  <h3>{repo.name}</h3>
  <a href="{repo.html_url}" target="_blank">{repo.full_name}</a>
  <p>LANGUAGE : {repo.language}</p>
</div>

<style>
   a{
      text-decoration: none;
      color: white;
  }
  div {
    height: 200px;
    width: 200px;
    margin: 10px;
    background: linear-gradient(45deg, #cc00ff, #d9055d);
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    transition: all 0.3s;
    padding: 15px;
  }
  div:hover {
    transform: scale(1.1);
    box-shadow: rgba(0, 0, 0, 0.25) 0px 14px 28px,
      rgba(0, 0, 0, 0.22) 0px 10px 10px;
  }
  h3{
      word-break: break-all;
  }

</style>
