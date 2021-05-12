<svelte:options tag="sf-agent" />

<script>
    import { createEventDispatcher } from 'svelte'
    import { get_current_component } from 'svelte/internal'

    export let postalcode
    export let clientid
    export let lob

    let checked

    const component = get_current_component()
    const svelteDispatch = createEventDispatcher()

    const dispatch = (name, detail) => {
        svelteDispatch(name, detail)
        component.dispatchEvent && component.dispatchEvent(new CustomEvent(name, { detail }))
    }

    const sendChangedEvent = () => {
        const event = {
            code: 'sfsta-ce1',
            description: 'change event 1 - new agent',
            data: {
                fname: 'Jim',
                lname: 'John',
            },
        }
        dispatch('change', event)
    }
</script>

<main>
    <h1>Hello {clientid} in {postalcode} for product {lob}</h1>

    <label>
        <input type="checkbox" {checked} on:click={sendChangedEvent} />
        Yes! Send events when you click me
    </label>
</main>

<style>
</style>
