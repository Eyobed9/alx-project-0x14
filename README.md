# alx-project-0x14
This is a repository for ALX Next.js project 

---

## 📘 API Overview

The **MoviesDatabase API** provides complete and up-to-date information on over 9 million movies, series, and episodes, as well as over 11 million actors, crew, and cast members. You can retrieve data such as titles, ratings, genres, seasons, episodes, biographies, YouTube trailer URLs, and much more. Ideal for building movie or series applications, this API ensures weekly updates for titles and daily updates for ratings.

---

## 🔢 API Version

**Version**: V1

---

## 🔗 Available Endpoints

| Endpoint                           | Description                                           |
| ---------------------------------- | ----------------------------------------------------- |
| `/titles`                          | Get an array of titles with filters or sorting.       |
| `/x/titles-by-ids`                 | Fetch multiple titles using a list of IMDb IDs.       |
| `/titles/{id}`                     | Get full details of a title using IMDb ID.            |
| `/titles/{id}/ratings`             | Get rating and vote count for a title.                |
| `/titles/series/{id}`              | Get all episodes of a series.                         |
| `/titles/seasons/{id}`             | Get the number of seasons in a series.                |
| `/titles/series/{id}/{season}`     | Get all episodes in a specific season.                |
| `/titles/episode/{id}`             | Get detailed info about a specific episode.           |
| `/titles/x/upcoming`               | Get a list of upcoming titles.                        |
| `/titles/search/keyword/{keyword}` | Search titles using a keyword.                        |
| `/titles/search/title/{title}`     | Search titles by title (supports exact match).        |
| `/actors`                          | Get a list of actors with pagination.                 |
| `/actors/{id}`                     | Get details of a specific actor.                      |
| `/title/utils/titleType`           | Get available title types.                            |
| `/title/utils/genres`              | Get available genres.                                 |
| `/title/utils/lists`               | Get available title list categories (like top-rated). |

---

## 📤 Request and Response Format

### ✅ Request Example (Fetch titles by keyword):

```http
GET /titles/search/keyword/inception
```

### ✅ Response Example:

```json
{
  "results": [
    {
      "id": "tt1375666",
      "titleText": { "text": "Inception" },
      "primaryImage": { "url": "..." },
      "releaseYear": { "year": 2010 },
      "genres": { "genres": [{ "text": "Action" }, { "text": "Sci-Fi" }] }
    },
    ...
  ],
  "page": 1,
  "next": 2,
  "entries": 10
}
```

---

## 🔐 Authentication

You must include your **API key** in the headers of every request:

```http
X-RapidAPI-Key: Hidden
X-RapidAPI-Host: moviesdatabase.p.rapidapi.com
```

Example with `fetch` in JavaScript:

```ts
const response = await fetch("https://moviesdatabase.p.rapidapi.com/titles", {
  headers: {
    "X-RapidAPI-Key": "YOUR_API_KEY",
    "X-RapidAPI-Host": "moviesdatabase.p.rapidapi.com"
  }
});
```

---

## ❗ Error Handling

| Status Code | Description                               |
| ----------- | ----------------------------------------- |
| 400         | Bad request – Check query parameters      |
| 401         | Unauthorized – Invalid or missing API key |
| 403         | Forbidden – You don’t have access         |
| 404         | Not found – Resource doesn’t exist        |
| 429         | Too many requests – Rate limit exceeded   |
| 500         | Internal server error – Try again later   |

> Always check for `!response.ok` and use `try/catch` blocks in your code.

---

## 📈 Usage Limits and Best Practices

* **Rate Limits**: As this API is hosted on RapidAPI, default free tier limits apply (typically 500–1000 requests/month depending on plan).
* **Max Results per Page**: 50
* **Best Practices**:

  * Use the `limit` and `page` parameters to paginate results
  * Use `info` parameter to reduce payload (`mini_info`, `image`, etc.)
  * Cache results where appropriate
  * Handle errors gracefully and retry with backoff when receiving `429` errors

---

