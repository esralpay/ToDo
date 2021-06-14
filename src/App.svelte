<script>
    import Form from "./Form.svelte";
    //document.body.style.backgroundColor = "red";
    document.body.style.backgroundImage = "url('https://i.ibb.co/B4Lnjky/todoBG.jpg')";

    $: toDos = JSON.parse(localStorage.getItem("localTodo"));
   
    const updateStorage = () => {
        localStorage.setItem("localTodo", JSON.stringify(toDos));
    }
    const addtoDo = (e) => {
        console.log(e.detail);
        const toDo = e.detail;
        toDos = [toDo, ...toDos];
        updateStorage();
    };


    const deleteObj = (i) => {
        let index = toDos.indexOf(i);
        toDos.splice(index, 1);
        toDos = toDos;
        updateStorage();
    };

    const updateObj = (i) => {
        let index = toDos.indexOf(i);
        if (toDos[index].isUpdate) {
            toDos[index].isUpdate = false;
        } else {
            toDos[index].isUpdate = true;
        }
        updateStorage();
    };
</script>

<main>
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.12.1/css/all.css" crossorigin="anonymous">
   
    <div class="todoContainer">
        <h1>TO DO LIST</h1>
       
        <Form on:addtoDo={addtoDo} />
        {#each toDos as toDo (toDo.id)}
            <div class={`toDoitem ${toDo.isChecked? "green" : ""}`}>
                <input class= "checkbox" type="checkbox" bind:checked={toDo.isChecked} />
               
                {#if toDo.isUpdate}
                    <input
                        type="text"
                        class="name"
                        placeholder={toDo.name}
                        bind:value={toDo.name}
                    />
                    <input
                        type="text"
                        class="details"
                        placeholder={toDo.details}
                        bind:value={toDo.details}
                    />
                {:else}
                    <div class="name">{toDo.name}</div>
                    <div class="details">{toDo.details}</div>
                {/if}
                <div class="buttons">
                    <button
                        class="deleteButton"
                        on:click={() => deleteObj(toDo)}><i class="fas fa-trash-alt"></i></button>
                    <button class="updateButton" on:click={() => updateObj(toDo)}>
                        {#if toDo.isUpdate}
                        <i class="fas fa-check"></i>
                        {:else}
                        <i class="fas fa-pen"></i>
                        {/if}
                    </button>
                </div>
            </div>
        {/each}
    </div>
</main>

<style>
    h1{
        -webkit-text-stroke: 1px rgba(49, 63, 66, 0.7);
        color:white;
    }
    .todoContainer {             
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        align-items: center;
        min-width: 600px;
        margin:40px 30%;
        background-color: rgba(125, 156, 163, 0.7);
        padding: 40px 50px;
        border-radius: 8px;              
        
            
    }
    .toDoitem {
        padding: 10px;
        display: flex;
        align-items: center;
        border: 2px rgba(0, 0, 0, 0.8) blue;
        border-radius: 4px;
        box-shadow: 2px 2px 6px rgba(0, 0, 0, 0.2);
        margin-top: 20px;
        width: 100%;
        background-color: rgba(125, 156, 163, 0.9);
    }
    .toDoitem:hover{
        background-color: rgba(179, 231, 233, 0.9);
    }
    .green {
        background-color: rgb(138, 190, 138);
    }
    .toDoitem:hover .buttons {
        visibility: visible;
    }
       
    .buttons {
        width: 100px;
    }
    .name {
        margin-left: 20px;
        width: 200px;
    }
    .details {
        flex: 1 1 0;
        min-width: 200px;
        margin-left: 20px;
    }
    .buttons {
        display: flex;
        visibility: hidden;
        justify-content: space-around;
        align-items: center;
    }
    .updateButton,
    .deleteButton {
        height: 40px;
        width: 40px;
    }
  

    .checkbox{
        min-width: 20px;
        min-height: 20px; 
    }
    .btn{
        font-size: 40px;
    }
  
</style>
