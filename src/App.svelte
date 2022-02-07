<script>
	//name it fullt customizable
  import { onMount } from "svelte";
  import Card from "./components/Card.svelte";
  let userData;
  let repoData = [];
  let filteredRepos = []
  let joining_date = ""
  onMount(() => {
    fetch(`https://api.github.com/users/hyvip-ai/repos?per_page=100`)
      .then((res) => res.json())
      .then((data) => {
        repoData = data;
		filteredRepos = [...repoData]
      });
  });
  fetch(`https://api.github.com/users/hyvip-ai`)
    .then((res) => res.json())
    .then((data) => {
      userData = data;
	  joining_date = `${new Date(userData?.created_at).getDate()}/${new Date(userData?.created_at).getMonth()+1}/${new Date(userData?.created_at).getFullYear()}`
	  
    });
  const filterRepos = (e) => {
	  
	  filteredRepos = repoData.filter(repo=>{
		  return repo.name.toLowerCase().includes(e.target.value.toLowerCase())
	  })
	  
  };
</script>

<main>
  <h1>HYVIP-AI GITHUB RESULTS</h1>
  <div
    style="display: flex; justify-content: space-between; align-items: center;margin-top: 25px;"
  >
    <div style="width: 45%;">
      <img src={userData?.avatar_url} alt="Rajat Mondal" />
    </div>
    <div style="width: 45%;">
      <p>NAME : {userData?.name}</p>
      <p>BIO : {userData?.bio}</p>
      <p>BLOG : <a href={userData?.blog}>{userData?.blog}</a></p>
      <p>Company : {userData?.company}</p>
      <p>Location : {userData?.location}</p>
      <p>Public Repos : {userData?.public_repos}</p>
	  <p>JOINED : {joining_date}</p>
    </div>
  </div>
  <h1>MY REPOS</h1>
  <input type="text" placeholder="SEARCH REPOS..." on:input={filterRepos} />
  <div class="cards">
    {#each filteredRepos as repo}
      <Card {repo} />
    {/each}
  </div>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 1.5em;
    font-weight: 100;
  }
  .cards {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
  }
  input {
    width: 60%;
    margin-bottom: 10px;
  }
</style>
