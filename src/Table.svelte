<script>   
    import materialStore from './material-store.js';

    let materials = [];   

    $: totalPrice = materials.reduce((acc, next) => {
        acc += next.price;
        return acc;
    }, 0)

    materialStore.subscribe(items => {
        materials = items;
    });

    const formatter = new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD'
    });
</script>


<style>
    table {
        width: 100%;
    }
</style>

<table class="primary">
    <thead>
        <tr>
            <th>Material</th>
            <th>Price</th>
            <th></th>
        </tr>
    </thead>
    <tbody>
        {#each materials as material (material.id)}
            <tr>
                <td>{material.name}</td>
                <td>{formatter.format(material.price)}</td>
                <td>
                    <i class="far fa-trash-alt"></i>
                </td>
            </tr>
        {/each}
        <tr>
            <td>Total</td>
            <td colspan="2">{formatter.format(totalPrice)}</td>
        </tr>
    </tbody>
</table>