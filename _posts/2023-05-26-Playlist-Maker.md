---
toc: true
layout: post
description: Test
categories: [markdown, project]
title: Find New Songs
---

<html>
<head>
    <title>Song Recommendation</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
    <h1>Song Recommendation</h1>
    <input type="text" id="songInput" placeholder="Enter a song title">
    <button onclick="recommendSongs()">Recommend</button>
    <div id="recommendations"></div>

  
<h1>Song Recommendation</h1>
<input type="text" id="songInput" placeholder="Enter a song title">
<button onclick="recommendSongs()">Recommend</button>
<div id="recommendations"></div>

<hr>

<h2>Add a Song to the Database</h2>
<input type="text" id="addTitleInput" placeholder="Song Title">
<input type="text" id="addArtistInput" placeholder="Artist">
<!-- Add more input fields for other attributes if needed -->
<button onclick="addSong()">Add Song</button>


<script>
        function recommendSongs() {
            var userInput = document.getElementById("songInput").value;
            recommendSimilarSongs(userInput);
        }

        function recommendSimilarSongs(title) {
            var features = ['bpm', 'energy', 'danceability', 'loudness', 'valence'];

            fetch('https://playourshiny.duckdns.org/songdatabase')
                .then(response => response.json())
                .then(data => {
                    var songData = data;

                    var inputIndex;
                    var inputSong = songData.find(function (song, index) {
                        if (song.title.toLowerCase() === title.toLowerCase()) {
                            inputIndex = index;
                            return true;
                        }
                        return false;
                    });

                    if (!inputSong) {
                        console.log("The title you entered is not in our database. Try another, or fix spelling");
                        return;
                    }

                    var similarities = songData.map(function (song, index) {
                        if (index === inputIndex) return Infinity; // Exclude the inputted song
                        return calculateSimilarity(inputSong, song);
                    });

                    var topIndices = getTopIndices(similarities, 5);

                    var recommendationsDiv = document.getElementById("recommendations");
                    recommendationsDiv.innerHTML = "<p>Based on the song you like: " + title + ", we recommend these five songs for your new playlist:</p><hr>";
                    for (var i = 1; i < topIndices.length + 1; i++) {
                        var index = topIndices[i - 1];
                        var recommendedSong = songData[index];
                        var songTitle = recommendedSong.title;
                        var songArtist = recommendedSong.artist;
                        var recommendation = document.createElement("p");
                        recommendation.textContent = i + ". " + songTitle + " by " + songArtist;
                        recommendationsDiv.appendChild(recommendation);
                    }
                })
                .catch(error => {
                    console.error("Error fetching data:", error);
                });
        }

        function calculateSimilarity(song1, song2) {
            var features = ['bpm', 'energy', 'danceability', 'loudness', 'valence'];
            var differences = features.map(function (feature) {
                return Math.abs(song1[feature] - song2[feature]);
            });
            return differences.reduce(function (sum, difference) {
                return sum + difference;
            }, 0);
        }

        function getTopIndices(arr, count) {
            var indices = arr.map(function (value, index) {
                return index;
            });
            indices.sort(function (a, b) {
                return arr[a] - arr[b];
            });
            return indices.slice(0, count);
        }

function addSong() {
        var title = document.getElementById("addTitleInput").value;
        var artist = document.getElementById("addArtistInput").value;
        // Get values for other attributes if needed

        var requestBody = {
            title: title,
            artist: artist,
            // Add other attributes as key-value pairs in the requestBody object
        };

        fetch('https://playourshiny.duckdns.org/create', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(requestBody)
        })
        .then(response => {
            if (response.ok) {
              alert("success")
                console.log("Song added successfully!");
                // Clear the input fields after successful addition
                document.getElementById("addTitleInput").value = "";
                document.getElementById("addArtistInput").value = "";
                // Clear other input fields if needed
            } else {
              alert(response.status)
                console.error("Failed to add song. Status:", response.status);
            }
        })
        .catch(error => {
            console.error("Error adding song:", error);
        });
    }

  
    </script>
</body>
</html>
