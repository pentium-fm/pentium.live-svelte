<script>
	export let current;
</script>



<style>



span {

    padding : 10px;
}



</style>

{#if current }

<span class="play"></span> Playing : {current.title}


{/if}
