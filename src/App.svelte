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

    currentEpIndex = index;
    if(currentEp)
    {
      audio.pause();
      audio.currentTime = 0;
      currentEpIndex = -1;
    }else{

    currentEp = items[index];

      audio.src = currentEp.audio;
      audio.play()
   

    }

	}

  


</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Lato");
@import url("https://fonts.googleapis.com/css?family=Roboto:400,700");
body {
  font-family: 'Lato', sans-serif;
  background: #222;
}

header {
  position: relative;
  box-sizing: border-box;
  padding: 40px;
  color: white;
  width: 100%;
  top: 0px;
  left: 0px;
      height: 55%;
  background: #232336;

}

.container-info {
  position: relative;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.summary-container {
  position: relative;
  align-self: flex-end;
  width: 50%;
  margin-left: 100px;
  margin-right: 25px;
  padding: 15px;
}
.summary-container #title {
  position: relative;
  display: inline-block;
  font-family: "Roboto", sans-serif;
  font-weight: 700;
  margin-bottom: 10px;
  font-size: 28px;
  letter-spacing: 1.5px;
  z-index: 2;
}
.summary-container #title:after {
  content: '';
  position: absolute;
  z-index: -1;
  width: 100%;
  bottom: 0px;
  left: 0px;
  height: 4px;
  background: linear-gradient(110deg, #e1f549, #29d0be, #6cb8ea, #ff5959);
}

.rating-container {
  position: absolute;
  top: 0px;
  right: 0px;
  display: flex;
  flex-direction: row;
  margin-right: 15px;
}

.star {
  position: relative;
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
  height: 20px;
  width: 20px;
  background: yellow;
  margin-top: 20px;
}

.show-summary {
  position: relative;
  line-height: 1.4;
}
.show-summary a {
  margin-left: 5px;
  text-transform: uppercase;
  color: #ccc;
}

.album {
  position: relative;
  height: 220px;
  width: 220px;
  background: purple;
  box-shadow: 0px 0px 20px 5px #111;
  z-index: 10;
}

.album:after {
  content: '';
  position: absolute;
  height: 100%;
  width: 100%;
  top: 0px;
  left: 0px;
  background-image: url(pentium-logo.jpg);
  background-size: 220px 220px;
}

.button-container {
  position: relative;
  top: 15px;
}

button {
  position: relative;
  background-color: #111;
  outline: none;
  border: none;
  color: white;
  cursor: pointer;
}

.podcast-button {
  position: relative;
  background-color: #111;
  outline: none;
  border: none;
  color: white;
  padding: 10px;
  font-size: 15px;
  font-family: "Roboto", sans-serif;
  letter-spacing: 2.5px;
  margin-right: 10px;
}
.podcast-button:last-child {
  margin-right: 0px;
}
.podcast-button:after {
  content: '';
  position: absolute;
  width: 100%;
  height: 3px;
  background: red;
  bottom: 0px;
  left: 0px;
  opacity: 0;
  transform: translateY(3px);
  transition: .5s;
}

.podcast-button:nth-child(1):after {
  background: #DEF06C;
}

.podcast-button:nth-child(2):after {
  background: #71C1D1;
}

.podcast-button:nth-child(3):after {
  background: #DD7171;
}

button:hover:after {
  opacity: 1;
  transform: translateY(0px);
}

.episode-list {
  box-sizing: border-box;
  position: relative;
  width: 100%;
  background: #222;
  color: white;
  display: flex;
  flex-direction: row;
  padding: 20px;
      height: 40%;

}
.episode-list:after {
  content: '';
  position: absolute;
  height: 7px;
  width: 100%;
  top: 0;
  left: 0;
  background: #444;
}

#row-one {
  position: relative;
  width: 66%;
  overflow-y:scroll;
}
#row-three {

	height : 5%;
color : white;
background-color : #111;

}
#episodes-header {
  position: relative;
  z-index: 15;
  font-size: 34px;
  font-family: "Roboto", sans-serif;
  font-weight: 700;
  letter-spacing: 3px;
  margin-top: 15px;
  width: 100%;
  top: 0px;
  left: 0px;
  margin-bottom: 3px;
}
#episodes-header:after {
  content: '';
  position: absolute;
  width: 100%;
  background: linear-gradient(110deg, #e1f549, #29d0be, #6cb8ea, #ff5959);
  height: 4px;
  bottom: -2px;
  left: 0px;
  z-index: -1;
}

.episode-container {
  position: relative;
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  width: 100%;
  border-bottom: 1px solid rgba(204, 204, 204, 0.2);
  cursor: pointer;
  transition: .4s;
}
.episode-container:hover {
  box-shadow: 0px 0px 2px 2px #111;
}

.episode-details-container {
  line-height: 1.5;
}
.episode-details-container h3 {
  font-size: 20px;
}
.episode-details-container h5 {
  color: rgba(204, 204, 204, 0.7);
}

.button-container-play {
  position: relative;
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
  top: 13px;
  left: 17px;
}

.stop {
  position: relative;
  margin-right: 15px;
  height: 45px;
  width: 45px;
  border-radius: 100%;
}
.stop:after {
  content: '';
  position: absolute;
  background: white;
  height: 19px;
  width: 19px;
    clip-path: polygon(48% 0, 100% 0, 100% 100%, 0 100%, 0 0);
  top: 13px;
  left: 13px;
}





.animation-square {
  position: absolute;
  height: 43px;
  width: 43px;
  left: 1px;
  top: 1px;
  border-radius: 10px;
}

.animation-square:nth-child(1) {
  background: #DEF06C;
}

.animation-square:nth-child(2) {
  background: #71C1D1;
}

.animation-square:nth-child(3) {
  background: #DD7171;
}

.animation-square:nth-child(2) {
  transform: rotate(22.5deg);
}

.animation-square:nth-child(3) {
  transform: rotate(45deg);
}

.episode-container:hover .button-container-play .animation-square:nth-child(1) {
  animation: rotate 6s ease infinite;
}
@keyframes rotate {
  50% {
    transform: rotate(120deg);
  }
  75% {
    transform: rotate(-90deg);
  }
  85% {
    transform: rotate(90deg);
  }
}
.episode-container:hover .button-container-play .animation-square:nth-child(2) {
  animation: rotate1 6s ease infinite;
}
@keyframes rotate1 {
  20% {
    transform: rotate(-90deg);
  }
  55% {
    transform: rotate(-30deg);
  }
  75% {
    transform: rotate(90deg);
  }
}
#row-two {
  position: relative;
  box-sizing: border-box;
  width: 33%;
  padding: 30px 0px 0px 45px;
}
#row-two h1 {
  font-size: 18px;
  text-align: left;
  border-bottom: 2px solid white;
}

textarea {
  box-sizing: border-box;
  display: block;
  width: 100%;
  margin-top: 10px;
  padding: 10px;
  background: #555;
  border: none;
  color: white;
  resize: none;
  height: 125px;
}
textarea:focus {
  outline: none;
}

.submit-container {
  position: relative;
  margin-top: 8px;
}

.rating-submit {
  position: absolute;
  display: inline-block;
  right: 0px;
  top: 0px;
}
.rating-submit .star {
  display: inline-block;
  margin-top: 10px;
}

@media screen and (max-width: 830px) {
  .episode-list {
    flex-direction: column;
  }

  #row-one {
    width: 100%;
  }

  #row-two {
    width: 100%;
    padding-left: 0px;
  }
}
@media screen and (max-width: 800px) {
  .container-info {
    flex-direction: column;
  }

  .summary-container {
    box-sizing: border-box;
    width: 100%;
    padding-left: 25px;
  }

  .album {
    left: 50%;
    transform: translateX(-50%);
  }


}

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

