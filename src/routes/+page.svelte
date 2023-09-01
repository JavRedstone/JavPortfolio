<style>

</style>
<main>
    <Paper variant="outlined" color="primary">
        <Title><b>Hi. My username is JavRedstone. Welcome to my portfolio.</b></Title>
        <Subtitle>I'm a high school student who loves to code programs ranging from small and simple to large and complex.</Subtitle>
    </Paper>
    <Paper variant="outlined" color="secondary" style="margin-top: 48px">
        <Title><b>My Github projects:</b></Title>
            {#await repos}
                <p>Loading Github Repositories...</p>
            {:then data}
                <LayoutGrid>
                    {#each data as repo}
                        <Cell>
                            <Card variant="outlined">
                                <Content>
                                    <h2>{repo.name}</h2>
                                    <p><b>{repo.description == null ? 'No description provided.' : repo.description}</b></p>
                                    <div><b><i>{repo.stargazers_count} {repo.stargazers_count != 1 ? 'stars' : 'star'}</i></b> | {repo.watchers_count} {repo.watchers_count != 1 ? 'watchers' : 'watcher'}</div>
                                    <div>{repo.forks_count} {repo.forks_count != 1 ? 'forks' : 'fork'} | {repo.open_issues_count} {repo.open_issues_count != 1 ? 'open issues' : 'open issue'}</div>
                                    {#if repo.language != null}
                                        <div>Made mainly in {repo.language}</div>
                                    {/if}
                                    {#if repo.license != null}
                                        <div>License: {repo.license.name}</div>
                                    {/if}
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

    import { onMount } from 'svelte';
    
    let repos: any = [];

    onMount(() => {
        repos = fetch('https://api.github.com/users/JavRedstone/repos').then((x) => x.json()).then((x) => x.sort(sortRepos));
        const sortRepos = (a: any, b: any) => {
            if (a.stargazers_count > b.stargazers_count) return -1;
            if (a.stargazers_count < b.stargazers_count) return 1;
            return 0;
        }
    });
</script>