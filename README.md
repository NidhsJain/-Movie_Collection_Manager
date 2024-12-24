# -Movie_Collection_Manager
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Movies List</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #1e1e2f;
            color: #f4f4f9;
            margin: 0;
            padding: 0;
        }

        header {
            background-color: #28293d;
            color: #fff;
            padding: 20px 0;
            text-align: center;
            font-size: 2.5em;
            font-weight: bold;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
        }

        .filters {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            align-items: center;
            gap: 15px;
            margin: 20px 0;
            padding: 10px;
            background-color: #2f2f40;
            border-radius: 8px;
        }

        .filters input, .filters select, .filters button {
            padding: 12px;
            font-size: 16px;
            border-radius: 5px;
            border: 1px solid #555;
            outline: none;
        }

        .filters input {
            flex: 1;
            max-width: 300px;
        }

        .filters button {
            background-color: #0078d7;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .filters button:hover {
            background-color: #005fb0;
        }

        .movie-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
            padding: 20px;
        }

        .movie-card {
            background-color: #28293d;
            border: 1px solid #333;
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .movie-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
        }

        .movie-card h3 {
            font-size: 1.8em;
            margin: 0;
            color: #f4f4f9;
        }

        .movie-card p {
            margin: 8px 0;
            font-size: 1.1em;
            color: #bbb;
        }

        .movie-card .rating {
            font-weight: bold;
            color: #ff9800;
        }

        .movie-card .year {
            font-size: 1em;
            color: #777;
        }

        .movie-card .genre {
            font-style: italic;
            color: #888;
        }

    </style>
</head>
<body>

    <header>
        Movies List
    </header>

    <div class="filters">
        <input type="text" id="searchBar" placeholder="Search by title...">
        <select id="genreFilter">
            <option value="All">All Genres</option>
            <option value="Sci-Fi">Sci-Fi</option>
            <option value="Action">Action</option>
        </select>
        <select id="sortFilter">
            <option value="rating">Sort by Rating</option>
            <option value="year">Sort by Year</option>
        </select>
        <button onclick="filterMovies()">Apply</button>
    </div>

    <div class="movie-container" id="movieContainer"></div>

    <script>
        const movies = [
            { title: "Inception", genre: "Sci-Fi", rating: 8.8, releaseYear: 2010 },
            { title: "The Dark Knight", genre: "Action", rating: 9.0, releaseYear: 2008 },
            { title: "Interstellar", genre: "Sci-Fi", rating: 8.6, releaseYear: 2014 },
            { title: "Tenet", genre: "Sci-Fi", rating: 7.5, releaseYear: 2020 }
        ];

        // Function to display movies in the movie container
        const displayMovies = (movieList) => {
            const movieContainer = document.getElementById("movieContainer");
            movieContainer.innerHTML = "";
            movieList.forEach(movie => {
                const movieCard = document.createElement("div");
                movieCard.classList.add("movie-card");

                movieCard.innerHTML = `
                    <h3>${movie.title}</h3>
                    <p class="genre"><strong>Genre:</strong> ${movie.genre}</p>
                    <p class="rating"><strong>Rating:</strong> ${movie.rating}</p>
                    <p class="year"><strong>Year:</strong> ${movie.releaseYear}</p>
                `;

                movieContainer.appendChild(movieCard);
            });
        };

        // Initial display of all movies
        displayMovies(movies);

        // Function to filter and sort movies
        const filterMovies = () => {
            const genre = document.getElementById("genreFilter").value;
            const searchQuery = document.getElementById("searchBar").value.toLowerCase();
            const sortBy = document.getElementById("sortFilter").value;

            let filteredMovies = movies;

            // Filter by genre
            if (genre !== "All") {
                filteredMovies = filteredMovies.filter(movie => movie.genre === genre);
            }

            // Filter by search query
            if (searchQuery) {
                filteredMovies = filteredMovies.filter(movie => movie.title.toLowerCase().includes(searchQuery));
            }

            // Sort by rating or year
            if (sortBy === "rating") {
                filteredMovies.sort((a, b) => b.rating - a.rating);
            } else if (sortBy === "year") {
                filteredMovies.sort((a, b) => b.releaseYear - a.releaseYear);
            }

            displayMovies(filteredMovies);
        };
    </script>

</body>
</html>
