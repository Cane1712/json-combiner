<script lang="ts">
    let input = $state('{"someFlag":"someValue"}');
    let json = $derived(JSON.parse(input) ?? {})
    let combined = $state({});

    function onclick() {
        combined = {...combined, ...json}
        input = "{}"
    }
</script>

<h1 class="text-2xl flex justify-center mt-8">JSON combiner</h1>
<div class="grid grid-cols-1 mx-auto justify-between mt-8 justify-items-center">
    <div class="columns-1">
        <h1 class="text-xl mx-auto">Load JSON</h1><br>
        <input bind:value={input}  type="text"><br><br>
        <button {onclick} class=" bg-blue-100">Add to selection</button> 
        <button class="bg-blue-100">Copy JSON</button>
    </div>
    <br>
</div>