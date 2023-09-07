 
# Image Search

This is a simple image search engine that allows users to search for images on the web.

## How to use

To use the image search engine, simply enter a search term into the search bar and click the "Search" button. The search results will be displayed below the search bar.

## Code snippets

The following code snippets show how to implement the image search engine:

html
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Image Search</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <h1>Image Search</h1>
    <form>
      <input type="text" id="search-input" placeholder="Search for images..." />
      <button id="search-button">Search</button>
    </form>
    <div class="search-results">
    </div>
    <button id="show-more-button">Show more</button>
    <script src="index.js"></script>
  </body>
</html>
```
css
```
body {
    margin: 0;
    font-family: sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;
    justify-content: center;
    background-size: cover;
    background-image: url("https://images.unsplash.com/photo-1575203091586-611fe505bb0e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxleHBsb3JlLWZlZWR8NHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=600&q=60");
    overflow: hidden;
  }
  
  h2 {
    text-transform: uppercase;
    letter-spacing: 4px;
    font-size: 14px;
    text-align: center;
    color: white;
  }
  
  .clock {
    display: flex;
  }
  
  .clock div {
    margin: 5px;
    position: relative;
  }
  
  .clock span {
    width: 100px;
    height: 80px;
    background: slateblue;
    opacity: 0.8;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 50px;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  }
  
  .clock .text {
    height: 30px;
    font-size: 10px;
    text-transform: uppercase;
    letter-spacing: 2px;
    background: darkblue;
    opacity: 0.8;
  }
  
  .clock #ampm {
    bottom: 0;
    position: absolute;
    width: 60px;
    height: 30px;
    font-size: 20px;
    background: green;
  }
```
js
```
const accessKey = "RZEIOVfPhS7vMLkFdd2TSKGFBS4o9_FmcV1Nje3FSjw";
const form = document.querySelector("form");
const searchInput = document.getElementById("search-input");
const searchResults = document.querySelector(".search-results");
const showMoreButton = document.getElementById("show-more-button");
let inputData = "";
let page = 1;
async function searchImages() {
  inputData = searchInput.value;
  const url = `https://api.unsplash.com/search/photos?page=${page}&query=${inputData}&client_id=${accessKey}`;
  const response = await fetch(url);
  const data = await response.json();
  if (page === 1) {
    searchResults.innerHTML = "";
  }
  const results = data.results;
  results.map((result) => {
    const imageWrapper = document.createElement("div");
    imageWrapper.classList.add("search-result");
    const image = document.createElement("img");
    image.src = result.urls.small;
    image.alt = result.alt_description;
    const imageLink = document.createElement("a");
    imageLink.href = result.links.html;
    imageLink.target = "_blank";
    imageLink.textContent = result.alt_description;
    imageWrapper.appendChild(image);
    imageWrapper.appendChild(imageLink);
    searchResults.appendChild(imageWrapper);
  });
  page++;
  if (page > 1) {
    showMoreButton.style.display = "block";
  }
}
form.addEventListener("submit", (event) => {
  event.preventDefault();
  page = 1;
  searchImages();
});
showMoreButton.addEventListener("click", () => {
  searchImages();
});

```
