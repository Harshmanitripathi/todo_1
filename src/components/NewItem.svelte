<script>
    import {createEventDispatcher} from "svelte";

    const dispatch = createEventDispatcher();
    let value = "";

    function handleKeyUp({key}) {
        if(key != "Enter" || value.length === 0) return;
        dispatch("newitem", value);
        value = "";
    }

    
</script>

<style>

</style>

<input type="text" on:keyup={handleKeyUp} 
bind:value placeholder="+ Add Item"> 