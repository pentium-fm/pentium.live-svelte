<script>
	export let current;
</script>



<style>

.played {
    padding : 10px;
    margin-left: 5px;
}


.play {
  position: relative;
  margin-right: 15px;
  height: 45px;
  width: 45px;
  border-radius: 100%;
}
.play:after {
  content: '';
  position: absolute;
  background: white;
  height: 20px;
  width: 25px;
  clip-path: polygon(62% 54%, 0 0, 0 100%);
  top: 0px;
  left: 0px;
}



</style>


{#if current }
<div class="played"> 
        <i class="play"></i>	&nbsp;	&nbsp;	&nbsp;Playing : {current.title}
</div>
{/if}
