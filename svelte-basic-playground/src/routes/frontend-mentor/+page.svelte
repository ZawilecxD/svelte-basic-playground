<script>
    const challenges = [
        {name: 'Results summary component', path: 'results-summary'}
    ];
</script>

<h1>Frontend mentor challenges 
    (<a href="https://www.frontendmentor.io/challenges?sort=difficulty|asc&types=free,free-plus" target="_blank">link</a>)
</h1>

<ul>
    {#each challenges as challenge}
    <li>
        <a href={`/frontend-mentor/${challenge.path}`}>{challenge.name}</a>
    </li>
    {/each}
</ul>
