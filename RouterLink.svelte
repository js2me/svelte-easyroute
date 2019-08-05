<a href={(window.routermode == 'hash' ? '/#' : '')+to} on:click={handleOnClickLink} class="{className}">
    {#if text && text !== ""}
        {text}
    {/if}
    <slot></slot>
</a>

<script>
    export let to
    export let text
    export let className
    export let activeClassName

    function handleOnClickLink(e) {
        e.preventDefault()
        e.stopPropagation()
        navigateRouter()
    }

    function navigateRouter() {
        if (window.routermode == 'hash') window.location.hash = to
        if (window.routermode == 'history') {
            let stateObj = { path: to, needAddBase: true };
            let event = new CustomEvent('svelteEasyrouteLinkClicked', 
                { 
                    'detail': stateObj
                });
            window.dispatchEvent(event)
        }
        if (window.routermode == 'silent') {
            let stateObj = { path: to, needAddBase: true };
            let event = new CustomEvent('svelteEasyrouteSilentNavigated', 
                { 
                    'detail': stateObj
                });
            window.dispatchEvent(event)
        }
    }
</script>
