
<style>



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
</style>

 <div class="review-container">
      <h1 id="review-header">Leave a Review</h1>
      <textarea></textarea>
      <div class="submit-container">
        <button class="podcast-button">Soon</button>

    </div>
    </div>
