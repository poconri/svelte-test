<script lang="ts">

let heroes:{
    name:string;
    id: number;
    images:{
        sm:string;
    };
    biography:{
        fullName:string;
    };
}[] = [];
let searchValue = '';

const fetchHeroes = () => {
    fetch('https://akabab.github.io/superhero-api/api/all.json')
        .then((res) => res.json())
        .then((data) => {
            heroes = data;
            console.log(heroes,'heroes')
        });
};
fetchHeroes();

$: filteredHeroes = heroes.filter(hero => 
    hero.name.toLowerCase().includes(searchValue.toLowerCase()) || hero.biography.fullName.toLowerCase().includes(searchValue.toLowerCase())
  );

</script>

<div class="HeroesList">
    <div
        class="container"
    >
        <h1>Heroes List</h1>
        <input type='text' bind:value={searchValue} placeholder="Search heroes by name">
        <div class="heroes-list">
            {#if searchValue.length > 0 && filteredHeroes.length === 0}
                <p>No heroes were found with the values provided</p>
            {:else if filteredHeroes.length > 0}
            {#each filteredHeroes as hero (hero.id)}
                <div class="hero-card">
                <img src={hero.images.sm} alt={hero.name}  class="hero-image"/>
                <div
                    class="hero-info"
                >
                    <h2 class="hero-name">{hero.name}</h2>
                    <h2 class="hero-name">{hero.biography.fullName}</h2>
                </div>
                
                </div>
            {/each}
        {:else}
            <p>Loading heroes...</p>
        {/if}
    </div>
    </div>
</div>

<style>
    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 16px;
    }

    .heroes-list {
        display: flex;
        width: 100%;
        flex-wrap: wrap;
        gap: 16px;
    }

    .hero-card {
        display: flex;
        gap: 16px;
    }
    
    .hero-info {
        display: flex;
        flex-direction: column;
    }

    .hero-name {
        width: 100px;
        flex-wrap: wrap;
    }

    .hero-image {
        width: 100px;
        height: 100px;
        object-fit: cover;
    }
</style>