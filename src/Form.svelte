<script>
    import materialStore from './material-store.js';

    export let id;
    export let name = "";
    export let price = 5;

    $: mode = id ? "edit" : "add";
    $: canSubmit = name !== "" && price >= 0;

    function submit() {
        if(!canSubmit) {
            return;
        }

        if (mode === "add") {
            materialStore.add(name, price);
        }

        price = 5;
        name = "";
        id = undefined;
    }

    function cancel() {
        price = 5;
        name = "";
        id = undefined;
    }
</script>


<style>
    button {
        margin-left: 20px;
    }

    button:disabled {
        cursor: not-allowed;
    }
</style>

<form on:submit|preventDefault={submit}>
    <fieldset>
        <label for="nameField">Material</label>
        <input bind:value={name} type="text" placeholder="Wood, Glue, Etc" id="nameField" />  

        <label for="priceField">Price</label>
        <input bind:value={price} min="0" step="any" type="number" placeholder="Price" id="priceField" />  
    
    </fieldset>
    <button disabled={!canSubmit} class="float-right" type="submit">{mode}</button>
  
    {#if (mode === 'edit')}
    <button on:click={cancel} class="float-right" type="button">Cancel</button>
    {/if}
</form>