<script>
    import { notify, modalStore, adageStore } from '../../store/app';
    import { createEventDispatcher } from 'svelte';
    import { fade, slide} from 'svelte/transition';
    import ButtonIcon from '../buttons/ButtonIcon.svelte';
    import ButtonSubmit from '../buttons/ButtonSubmit.svelte';

    const dispatch = createEventDispatcher();

    let adage = "";
    let uniqueTo = "";

    const handleSubmit = async (event) => {
        event.preventDefault();
        const result = await adageStore.addAdage(adage , uniqueTo, $adageStore.page)
        if(result.added === true && result.error === false){
            modalStore.set({shouldDisplay: "", canClickNext: true})
        } 
    }
</script>

<section class="modal-comp" transition:fade>
    <div class="flex-inline">
        <h2>Add Adage</h2>
        <ButtonIcon on:click={()=>dispatch('close')}><i class="fa-solid fa-times"></i></ButtonIcon>
    </div>
    <form method="post" transition:slide|local on:submit={handleSubmit}>
        <div class="input-group">
            <label for="adage">Adage</label>
            <div class="field">
                <textarea bind:value={adage} cols="40" rows="6"></textarea>
            </div>
        </div>

        <div class="input-group">
            <label for="country">Unique to</label>
            <div class="field">
                <input type="text" bind:value={uniqueTo} id="country" list="countries" placeholder="nigerian">
                <datalist id="countries">
                    <option value="Nigerian"></option>
                    <option value="Kenyan"></option>
                    <option value="South African"></option>
                    <option value="Nigerian"></option>
                    <option value="Nigerian"></option>
                </datalist>
            </div>
        </div>

        <div class="input-group">
            <label for="tags">Tags</label>
            <div class="field">
                <i class="fa-solid fa-hashtag"></i>
                <input type="email" name="tags" id="tags" placeholder="wisdon, life, joy, ...">
            </div>
        </div>

        <ButtonSubmit><i class="fa-solid fa-plus"></i> <span>Add Adage</span></ButtonSubmit>
    </form>
</section>


<style>
    .flex-inline {
        margin-bottom: 2rem;
    }
    h2 {
        text-align: left;
        color: hsl(var(--clr-secondary));
    }
</style>