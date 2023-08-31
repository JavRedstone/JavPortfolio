<style>

</style>
<main>
    <Paper color="primary" variant="outlined">
        <Title><b style="color: #f44336">Hi. My username is JavRedstone. Welcome to my portfolio.</b></Title>
        <Subtitle style="color: #f44336">I'm a high school student who loves to code programs ranging from small and simple to large and complex.</Subtitle>
    </Paper>
    <Paper variant="outlined" style="margin-top: 48px">
        <Title><b>My Github projects:</b></Title>
            {#await repos}
                <p>Loading Github Repositories...</p>
            {:then data}
                <LayoutGrid>
                    {#each data as repo}
                        <Cell>
                            <Card variant="outlined" style="border-color: {repo.stargazers_count > 1 ? '#2196f3' : ''}; background-color: {repo.stargazers_count > 1 ? '#2196f333' : ''}">
                                <Content>
                                    <h3>{repo.name}</h3>
                                    <p>{repo.description == null ? 'No description provided.' : repo.description}</p>
                                    <div>{repo.stargazers_count} {repo.stargazers_count != 1 ? 'stars' : 'star'} | {repo.watchers_count} {repo.watchers_count != 1 ? 'watchers' : 'watcher'}</div>
                                    <ActionButtons>
                                        <Button color="secondary" href={repo.html_url} target="_blank" rel="noopener noreferrer">View on Github</Button>
                                    </ActionButtons>
                                </Content>
                            </Card>
                        </Cell>
                    {/each}
                </LayoutGrid>
            {:catch error}
                <p>Failed to load Github Repositories. Perhaps you have been ratelimited. Try again later.</p>
            {/await}
    </Paper>
</main>
<script lang="ts">
    import Paper, { Title, Subtitle } from '@smui/paper';
    import LayoutGrid, { Cell } from '@smui/layout-grid';
    import Card, { Content , ActionButtons} from '@smui/card';
    import Button from '@smui/button';
    
    // sort by stargazers_count
    let repos = fetch('https://api.github.com/users/JavRedstone/repos').then((x) => x.json()).then((x) => x.sort(sortRepos));
    const sortRepos = (a: any, b: any) => {
        if (a.stargazers_count > b.stargazers_count) return -1;
        if (a.stargazers_count < b.stargazers_count) return 1;
        return 0;
    }
</script>