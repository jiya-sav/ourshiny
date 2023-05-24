
<html>
<body>
<form id="uinput" action="#">
  Enter the ingredient you are allergy to: <input type="text" name="allergy"
  id="allergy"><br>
  Enter the product you were recommended: <input type="text" name="product" id="product"><br>
  <input type=button onclick="allergyCheck()" value="Submit">
</form>
</body>

<p id="out"></p>


<script>
// Function to recommend similar songs based on a given song
function recommendSimilarSongs(title, songData) {
  // Find the song with the given title
  const song = songData.find(song => song.Title === title);

  if (!song) {
    console.log("Song not found.");
    return;
  }

  // Print the input title and its features
  console.log(`\nFeatures of '${title}':`);
  for (const feature in song) {
    console.log(`${feature}: ${song[feature]}`);
  }

  // Calculate the similarity score between the given song and all other songs
  const similarities = songData.map(otherSong => {
    const commonFeatures = ["Danceability", "Liveness", "Popularity", "Energy", "Beats Per Minute (BPM)"];
    const songFeatures = commonFeatures.map(feature => song[feature]);
    const otherSongFeatures = commonFeatures.map(feature => otherSong[feature]);
    const similarity = calculateSimilarity(songFeatures, otherSongFeatures);
    return { song: otherSong, similarity };
  });

  // Sort the songs by similarity in descending order
  similarities.sort((a, b) => b.similarity - a.similarity);

  // Print the top 5 recommended songs and their features
  console.log(`\nRecommendations based on '${title}':`);
  for (let i = 0; i < 5; i++) {
    const recommendedSong = similarities[i].song;
    console.log(`\n${i + 1}. ${recommendedSong.Title} by ${recommendedSong.Artist}`);
    console.log("Features:");
    for (const feature in recommendedSong) {
      if (commonFeatures.includes(feature)) {
        console.log(`${feature}: ${recommendedSong[feature]}`);
      }
    }
  }
}

// Calculate cosine similarity between two vectors
function calculateSimilarity(vector1, vector2) {
  const dotProduct = vector1.reduce((acc, val, i) => acc + val * vector2[i], 0);
  const magnitude1 = Math.sqrt(vector1.reduce((acc, val) => acc + val * val, 0));
  const magnitude2 = Math.sqrt(vector2.reduce((acc, val) => acc + val * val, 0));
  return dotProduct / (magnitude1 * magnitude2);
}

// Fetch the song data from the local URL
fetch("http://10.169.55.42:8080/songdatabase")
  .then(response => response.json())
  .then(songData => {
    // Prompt the user to input a song title
    const title = prompt("Enter a song title:");

    // Call the recommendSimilarSongs function with the user's input and the song data
    console.log(`Based on the song you like: ${title}, we recommend these five songs for your new playlist:`);
    recommendSimilarSongs(title, songData);
  })
  .catch(error => console.log("Error fetching song data:", error));
</script>