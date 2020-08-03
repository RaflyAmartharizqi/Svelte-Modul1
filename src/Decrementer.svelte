<script>
    import {store} from "./store";

    function decrement() {
        store.update(n =>  n++);
    }
</script>

<button on:click={decrement}>-</button>