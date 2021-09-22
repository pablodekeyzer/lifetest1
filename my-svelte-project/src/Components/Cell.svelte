<script lang="ts">
 export let alive
 export let c
 export let r
 console.log(c,r)
</script>

<div>
    <div class="{ alive ? 'alive': '' }">
    </div>
</div>

<style>
    div {
        display: flex;
        flex-direction: row;
        width: 3rem;
        height: 3rem;
        border: solid black 1px;
        margin: 0;
        padding: 0;
    }
    .alive {
        background: black;
    }
</style>
