<script lang="ts">
import Counter from './Counter.svelte'
let counterInfos: {
    title: string,
    count: number
} [] = [{
    title: 'new',
    count: 0
}]

function addCounter() {
    counterInfos = [...counterInfos, {
        title: 'new',
        count: 0
    }];
}

function removeCounter(index: number) {
    counterInfos = counterInfos.filter((_, i) => i !== index);
}

function updateInfo(index: number, data: {
    key: string,
    value: string | number
}) {
    const {
        key,
        value
    } = data;
    counterInfos[index][key] = value;
}
</script>

<main>
    <h1>Multiple Counter</h1>
    {#each counterInfos as counterInfo, i}
    <Counter {counterInfo} on:remove={() => removeCounter(i)} on:update={(event) => updateInfo(i, event.detail) }/>
        {/each}
        <button class="add-counter" on:click={addCounter}>new counter</button>
        Title list: {#each counterInfos as counterInfo, i}
        <letter>Counter {i} : [title : {counterInfo.title}, count: {counterInfo.count}]</letter>
        {/each}
        <p>Total Counter: {
            counterInfos.reduce((total, obj) =>
            total + obj.count
            ,0)
            }
        </p>
        <p>2023.12.18 @ Joah Mack</p>
        </main>

<style>
main {
    text-align: center;
    max-width: 450px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    gap: 10px;
}

main letter {
    word-wrap: break-word;
    overflow-wrap: break-word;
    text-align: left;
}

button.add-counter {
    background-color: rgb(71, 188, 71);
    color: white;
    outline: none;
    border: none;
    cursor: pointer;
    box-shadow: 1px 2px 10px grey;
}

button.add-counter:hover {
    background-color: rgb(44, 145, 44);
}
</style>
