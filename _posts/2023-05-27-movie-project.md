---
toc: true
layout: post
description: Find a movie!
categories: [markdwon]
title: Movie Mashup 

---

<html>
<head>
    <title>Random Movie Generator</title>
    <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Random Movie Generator</h1>
        <button id="randomizeBtn">Randomize</button>
        <div id="movieDetails">
            <p id="movieType"></p>
            <h2 id="movieTitle"></h2>
            <p id="listedIn"></p>
            <p id="rating"></p>
            <p id="description"></p>
        </div>
    </div>

 <script src="script.js"></script>
</body>
</html>

<style>
.container {
    max-width: 500px;
    margin: 0 auto;
    text-align: center;
    padding: 20px;
}

h1 {
    margin-top: 0;
}

button {
    font-size: 18px;
    padding: 10px 20px;
    margin-bottom: 20px;
}

#movieDetails {
    display: none;
}

#movieTitle {
    margin-top: 0;
}

p {
    margin: 10px 0;
}

</style>

<script>

document.getElementById("randomizeBtn").addEventListener("click", randomizeMovie);

function randomizeMovie() {
    fetch("files/netflix_titles.csv")
        .then(response => response.text())
        .then(data => {
            const movies = data.split("\n").slice(1); // Skip the header line
            const randomIndex = Math.floor(Math.random() * movies.length);
            const randomMovie = movies[randomIndex].split(",");

            const movieType = randomMovie[1].trim();
            const movieTitle = randomMovie[2].trim();
            const listedIn = randomMovie[10].trim();
            const rating = randomMovie[8].trim();
            const description = randomMovie[11].trim();

            document.getElementById("movieType").textContent = `Type: ${movieType}`;
            document.getElementById("movieTitle").textContent = movieTitle;
            document.getElementById("listedIn").textContent = `Listed In: ${listedIn}`;
            document.getElementById("rating").textContent = `Rating: ${rating}`;
            document.getElementById("description").textContent = `Description: ${description}`;

            document.getElementById("movieDetails").style.display = "block";
        })
        .catch(error => {
            console.log("Error:", error);
        });
}

</script>

