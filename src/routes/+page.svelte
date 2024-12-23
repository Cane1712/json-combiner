<script lang="ts">
    let input = $state('{"someFlag":"someValue"}');
    let button: HTMLButtonElement;
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

    async function validateJSON() {
        const allflags = await fetch("https://clientsettings.roblox.com/v2/settings/application/PCDesktopClient").then(res => res.json());
        button.innerHTML = `Validate JSON (${Object.keys(combined).filter(key => allflags[key] == undefined).length === 0})`
        // return Object.keys(combined).filter(key => allflags[key] == undefined).length === 0;
    }
</script>

<h1 class="text-2xl flex justify-center mt-8">JSON combiner</h1>
<div class="grid grid-cols-1 mx-auto grid-col mt-8 justify-items-center">
    <div class="mb-8">
        <button {onclick} class=" bg-blue-100 w-40">Combine JSON</button><br> <br>
        <button onclick={async (e) => {await navigator.clipboard.writeText(JSON.stringify(combined))}} class="bg-blue-100 w-40">Copy JSON</button>
        <button bind:this={button} onclick={async (e) => await validateJSON()}>Validate JSON</button>
    </div>
    <div>
        <!-- <h1 class="text-xl mx-auto">Load JSON</h1><br> -->
        <textarea bind:value={input} class="w h"> </textarea><br><br>
    </div>
    <br>
</div>

<style>
    /* button {
        width: 4rem !important;
    } */

    .w {
        width: 30rem
    } 
    .h {
        height: 12em;
    }
</style>