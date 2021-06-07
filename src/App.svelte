<script>
    import Form from "./Form.svelte";
    let toDos = [
        {name: "Discover", details:"The measurement of Corte Vecchio (the courtyard in the duke’s palace).", id:0},
        {name: "Calculate", details:"The measurement of Milan and Suburbs", id:1}
    ]
    const addtoDo = (e) => {
        console.log(e.detail);
        const toDo = e.detail;
        toDos = [toDo,...toDos]
    }

</script>
<main>
    <Form on:addtoDo = {addtoDo}/>
    {#each toDos as toDo (toDo.id)}
        <div class="toDoitem">
            <h4>{toDo.name}</h4>
            <h4>{toDo.details}</h4>

        </div>

    {/each}

</main>
<style>
    .toDoitem {
		display: flex;       
        align-items: flex-start;
        border: 2px solid gray;
        text-align: left;
        padding: 8px;
        margin-top: 20px;        
        width: 80% ;
    }
    main {
        display: flex;
        flex-direction: column;
        align-items:flex-start;
		margin-left: 250px;
		padding: 8px;
    }
	h4{
		padding-left: 20px;
	}
    

</style>