<script>

    import { createEventDispatcher } from "svelte";

    export let id, text, completed;

    const dispatch = createEventDispatcher();

    function triggerUpdate() {
        dispatch ("update", { id, text, completed });
    }

    function handleDoubleClick(){
        const yes = confirm("Are you sure to delete");

        if(yes) {
            dispatch("delete", id);
        }
    }
</script>

<style>

.item.completed {
    background: #dddddd;
}

.item.completed .text-input {
    color: #555555;
    text-decoration: line-through;
}

</style>

<div class="item" class:completed on:dblclick={handleDoubleClick}>
    <input 
    class="text-input"
    type="text"
    bind:value={text}
    readonly={completed}
    on:keyup={({key, target}) => key === 'Enter' && target.blur()}
    on:blur={() => triggerUpdate}
    />

    <input
    class="completed-checkbox" type="checkbox" bind:checked={completed}
    on:change={()=> triggerUpdate()} />
</div>