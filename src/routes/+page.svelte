<script lang="ts">
    let input = $state('{"someFlag":"someValue"}');
    let json = $derived.by(() => {
        try {
            return JSON.parse(input) ?? {};
        } catch {
            return {};
        }
    })
    let combined = $state({});

    function onclick() {
        combined = {...combined, ...json}
        input = "{}"
    }

</script>

<h1 class="text-2xl flex justify-center mt-8">JSON combiner</h1>
<div class="grid grid-cols-1 mx-auto grid-col mt-8 justify-items-center">
    <div class="mb-8">
        <button {onclick} class=" bg-blue-100">Combine JSON</button><br> <br>
        <button onclick={async (e) => {await navigator.clipboard.writeText(JSON.stringify(combined))}} class="bg-blue-100">Copy JSON</button>
    </div>
    <div>
        <!-- <h1 class="text-xl mx-auto">Load JSON</h1><br> -->
        <textarea bind:value={input} class="w h"> </textarea><br><br>
    </div>
    <br>
</div>

<style>
    .w {
        width: 30rem
    } 
    .h {
        height: 12em;
    }
</style>