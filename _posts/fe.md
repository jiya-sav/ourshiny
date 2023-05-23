<!DOCTYPE html>
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

    <script>
        function recommendSongs() {
            var userInput = document.getElementById("songInput").value;
            
            fetch('http://172.25.189.122:8080/songdatabase')  // Replace with your actual backend API link
                .then(response => response.json())
                .then(data => {
                    // Filter the songs based on the user's input
                    var filteredSongs = data.filter(song => song.title.toLowerCase().includes(userInput.toLowerCase()));
                    
                    // Sort the filtered songs based on all keys dynamically
                    var sortedSongs = mergeSort(filteredSongs);
                    
                    // Display the top 5 recommended songs
                    var recommendationsDiv = document.getElementById("recommendations");
                    recommendationsDiv.innerHTML = "";
                    for (var i = 0; i < Math.min(sortedSongs.length, 5); i++) {
                        var song = sortedSongs[i];
                        var songTitle = song.title;
                        var songArtist = song.artist;
                        var recommendation = document.createElement("p");
                        recommendation.textContent = "Title: " + songTitle + ", Artist: " + songArtist;
                        recommendationsDiv.appendChild(recommendation);
                    }
                })
                .catch(error => {
                    console.error("Error fetching data:", error);
                });
        }
        
        // Merge sort implementation
        function mergeSort(arr) {
            if (arr.length <= 1) {
                return arr;
            }
            
            var mid = Math.floor(arr.length / 2);
            var left = mergeSort(arr.slice(0, mid));
            var right = mergeSort(arr.slice(mid));
            return merge(left, right);
        }
        
        function merge(left, right) {
            var result = [];
            var i = 0, j = 0;
            
            while (i < left.length && j < right.length) {
                var compare = compareKeys(left[i], right[j]);
                if (compare < 0) {
                    result.push(left[i++]);
                } else {
                    result.push(right[j++]);
                }
            }
            
            while (i < left.length) {
                result.push(left[i++]);
            }
            
            while (j < right.length) {
                result.push(right[j++]);
            }
            
            return result;
        }
        
        function compareKeys(song1, song2) {
            var keys = Object.keys(song1);
            for (var i = 0; i < keys.length; i++) {
                var key = keys[i];
                if (song1[key] !== song2[key]) {
                    return song1[key] - song2[key];
                }
            }
            return 0;
        }
    </script>
</body>
</html>
