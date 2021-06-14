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
        name = "";
        details="";
    }; 

</script>
<form class="form" on:submit|preventDefault ={handleSubmit}>
    <input type="text" placeholder="to do" bind:value={name}>
    <input type="text" placeholder="details" bind:value={details}>
    <button class="addButton">Add</button>
    
</form>
<style>
    .addButton{
        width:80px;
    }
    .form{

        margin-top: 50px;
        margin-bottom: 50px;        
    }

</style>