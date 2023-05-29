---
toc: true
layout: post
description: Test
categories: [markdown, project]
title: Find New Songs
---

<html>
<head>
	<title>Recommended Songs</title>
	<style>
		.container {
			max-width: 800px;
			margin: 0 auto;
		}

		.table-container {
			overflow-x: auto;
		}

		table {
			width: 100%;
			border-collapse: collapse;
		}

		th, td {
			padding: 8px;
			text-align: left;
			border-bottom: 1px solid #ddd;
			white-space: nowrap;
			overflow: hidden;
			text-overflow: ellipsis;
		}

		th {
			background-color: #f2f2f2;
		}
	</style>
</head>
<h2>Enter a song you like</h2>
<input id="song"><button onclick="findRecommendations()">Enter</button>
<body>
	<div class="container">
		<h2>Recommended Songs Based on Song You Like</h2>
		<div class="table-container">
			<table>
				<thead>
					<tr>
						<th>#</th>
						<th>Title</th>
						<th>Artist</th>
						<th>URL</th>
					</tr>
				</thead>
				<tbody>
					<!-- Table data will be dynamically generated here -->
				</tbody>
			</table>
		</div>
	</div>

<script>
	async function findRecommendations() {
        const song = document.getElementById("song").value
        const modifiedSong = song.replace(/ /g, "%20")
        console.log(modifiedSong)
		const _url = `https://shazam.p.rapidapi.com/search?term=${song}&locale=en-US&offset=0&limit=1`;
		const _options = {
			method: 'GET',
			headers: {
				'X-RapidAPI-Key': '4abcb54450msh7468dfd72294e89p18fbaajsn6d4200063b39',
				'X-RapidAPI-Host': 'shazam.p.rapidapi.com'
			}
		};

		try {
			const response = await fetch(_url, _options);
			const _result = await response.json(); // Parse the response as JSON
			const key = _result.tracks.hits[0].track.key; // Access the "key" property
			console.log(key);

			const url = `https://shazam.p.rapidapi.com/songs/list-recommendations?key=${key}&locale=en-US`;
			const options = {
				method: 'GET',
				headers: {
					'X-RapidAPI-Key': '4abcb54450msh7468dfd72294e89p18fbaajsn6d4200063b39',
					'X-RapidAPI-Host': 'shazam.p.rapidapi.com'
				}
			};

			async function fetchData() {
				try {
					const response = await fetch(url, options);
					const result = await response.json();

					if (result.tracks) {
						let tableHTML = '';

						result.tracks.forEach((track, index) => {
							tableHTML += `
								<tr>
									<td>${index + 1}</td>
									<td>${track.title}</td>
									<td>${track.subtitle}</td>
									<td><a href="${track.url}" target="_blank">Listen</a></td>
								</tr>`;
						});

						document.querySelector('.table-container tbody').innerHTML = tableHTML;
					} else {
						console.log('API request failed.');
					}
				} catch (error) {
					console.error(error);
				}
			}

			fetchData();
		} catch (error) {
			console.error(error);
		}
	}
</script>

</body>
</html>