<script>
    import {createEventDispatcher} from 'svelte';
    import {fly} from 'svelte/transition'
    export let status = "";
    export let reason = "";

    const dispatch = createEventDispatcher();
</script>

<section class="toast warning" in:fly="{{x: 200, duration: 230}}" out:fly="{{x: 200, duration: 230}}">
    <div class="flex-inline">
        <p class="status">{status}</p>
        <span class="close" on:click={()=>dispatch('closeToast')}> <i class="fa-solid fa-times"></i></span>
    </div>
    <p class="reason">{reason}</p>
</section>

<style>
    .toast {
        position: fixed;
        top: 10%;
        right: 6%;
        padding: 1rem;
        border-radius: 0.5rem;
        background-color: whitesmoke;
        color: var(--clr-background);
        z-index: 10;
        width: 230px;
        min-height: 80px;
        display: flex;
        flex-direction: column;
        align-content: center;
        gap: 1rem;
        border: solid var(--clr-background) 2px;
    }
    .status {
        font-size: 1.4rem;
        font-weight: var(--fw-800);
        font-family: var(--ff-secondary);
        text-transform: capitalize;
    }
    .close {
        width: 32px;
        height: 32px;
        background-color: var(--clr-background);
        color: var(--clr-accent);
        border-radius: 4px;
        cursor: pointer;
        display: grid;
        place-content: center;
    }
    .reason {
        text-align: left;
    }
</style>