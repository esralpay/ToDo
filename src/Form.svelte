<script>
    import {createEventDispatcher} from "svelte";
    let dispatch = createEventDispatcher();
    let name;
    let details;
    const handleSubmit= () => {
        const toDo = {
            name:name,
            details:details,
            id:Math.random()
        }
        console.log(toDo);
        dispatch("addtoDo",toDo);
    }; 

</script>
<form on:submit|preventDefault ={handleSubmit}>
    <input type="text" placeholder="to do" bind:value={name}>
    <input type="text" placeholder="details" bind:value={details}>
    <button>Add</button>
</form>
<style>

</style>