<script>


let items = [];
let currentEp = null;
let audio = document.createElement('audio');
let currentEpIndex = -1 ;

import Current from './Current.svelte';
import Review from './Review.svelte';



fetch("https://anchor.fm/s/889f12c/podcast/rss")
      .then(response => response.text())
      .then(xml => {
        let parser = new DOMParser();
        let document = parser.parseFromString(xml, "application/xml");
        // set array of items
        items = Array.from(document.getElementsByTagName("item")).map(
          item => {
            return {
              guid: item.querySelector("guid").textContent,
              title: item.querySelector("title").textContent,
              description: item
                .querySelector("description")
                .textContent.replace(/(<([^>]+)>)/gi, ""),
              pubDate: item.querySelector("pubDate").textContent,
              audio: item.querySelector("enclosure").getAttribute("url"),
            };
          }
        );
  });

  function playMe(index) {



    
    if(currentEp)
    {

      audio.pause();
      audio.currentTime = 0;


      if(index === currentEpIndex){
      currentEp = null;
      currentEpIndex = -1;
      }else{

      currentEp = items[index];
      currentEpIndex = index;
      audio.src = currentEp.audio;
      audio.play();

      }


    }else{


      currentEp = items[index];
      currentEpIndex = index;
      audio.src = currentEp.audio;
      audio.play();
      
   

    }

	}

  


</script>

<style>
@import url("main.css");


</style>


<header>
  <div class="container-info">
    <div class="album"></div>
    <div class="summary-container">
      <h1 id="title">About the podcast</h1>
      <p class="show-summary">
	  
	      Pentium radio (formerly Typehints) is a Moroccan podcast (Moroccan
            dialect aka Darija) hosted by{" "}
            <b>
              
              <a href="https://twitter.com/JefferyHus">Hussein Jeffery</a>
            </b>
            and
            <b>
              <a href="https://github.com/AbderrahimSoubaiElidrissi">Abderrahim Soubai</a>
            </b>
            interested in web development and software engineering culture.

	  
	  </p>




      <div class="button-container">
        <button class="podcast-button">Subscribe</button>
        <button class="podcast-button">Donate</button>
      </div>
    </div>
  </div>
</header>
<div class="episode-list">

  <div class="row" id="row-one">
    <h1 id="episodes-header">Episodes</h1>





 
 
     {#each items as item, i}
    <div class="episode-container">

      <div class="episode-details-container">
        <h3>{item.title}</h3>
        <h5>{item.description} - {item.pubDate}</h5>

      </div>
      <div class="button-container-play">
        <div class="animation-square"></div>
        <div class="animation-square"></div>
        <div class="animation-square"></div>
        <button on:click={e => playMe(i)}  class='{ i === currentEpIndex ? "stop": "play"}'></button>
      </div>
    </div>
 	{/each}


</div>
  <div class="row" id="row-two">
  <Review />
</div>
</div>

    <div class="" id="row-three">



<Current current={currentEp} />
        



	</div>

