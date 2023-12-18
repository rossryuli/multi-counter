<script lang="ts">
    import {createEventDispatcher} from 'svelte'
	export let counterInfo: {title: string, count: number};
    const dispatch = createEventDispatcher()
    function incCount() {
        counterInfo.count += 1 ;
        update({key: 'count', value: counterInfo.count})
    }
    function decCount() {
        counterInfo.count > 0 ? counterInfo.count -= 1 : 0;
        update({key: 'count', value: counterInfo.count})
    }
    function clearCount() {
        counterInfo.count = 0;
        update({key: 'count', value: counterInfo.count})
    }
    function removeCount() {
        dispatch('remove')
    }
    function onChange(event) {
        const {name, value} = event.target;
        update({key: name, value: value})
    }
    function update(data: {key: string, value: string | number}) {
        dispatch('update', data)
    }
</script>

<main>
<div class="board">
    <div>
        <input type="text" name="title" bind:value={counterInfo.title} on:input={onChange}/>
    </div>
    <div>
        <strong>{counterInfo.count}</strong>
    </div>
    <div>
        <button class="inc" on:click={incCount}>+</button>
        <button class="dec" on:click={decCount}>-</button>
        <button class="clear" on:click={clearCount}>0</button>
        <button class="remove" on:click={removeCount}>x</button>
    </div>
    
</div>
</main>

<style>
.board {
    padding: 10px;
    background-color: #f3f3f3;
    display: flex;
    align-items: center;
    justify-content: space-around;
    border-radius: 20px;
    box-shadow: 1px 2px 10px grey;
}
input {
    border: 1px solid #f3f3f3;
    outline: none;
    margin: 0;
}
input:focus {
    border: 1px solid #9f9f9f
}
button {
    cursor: pointer;
    margin: 0;
    width: 30px;
    height: 30px;
    line-height: 1.0;
    border: none;
    outline: none;
    color: white;
    background-color: transparent;
}
button.inc {
    background-color: rgb(205, 49, 49);
}
button.inc:hover {
    background-color: rgb(138, 11, 11);
}
button.dec {
    background-color: rgb(74, 74, 246);
}
button.dec:hover {
    background-color: rgb(19, 19, 138);
}
button.clear {
    background-color: rgb(194, 194, 58);
}
button.clear:hover {
    background-color: rgb(111, 111, 14);
}
button.remove {
    color: rgb(196, 28, 81);
    transition: 0.2s;
}
button.remove:hover {
    scale: 1.2;
    font-weight: bold;
}
</style>