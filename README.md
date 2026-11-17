# 🎬 MovieCatalogApi

A **RESTful Web API** for managing a movie catalogue, built with **ASP.NET Core** and **Entity Framework Core**, with interactive documentation through **Swagger**.

![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet&logoColor=white)
![ASP.NET Core Web API](https://img.shields.io/badge/ASP.NET%20Core-Web%20API-5C2D91)
![EF Core](https://img.shields.io/badge/EF%20Core-9.0-6DB33F)
![Swagger](https://img.shields.io/badge/Swagger-OpenAPI-85EA2D?logo=swagger&logoColor=black)

---

## 📖 Overview

MovieCatalogApi is the **back-end** of a two-part project. It exposes CRUD endpoints to create, read, update and delete movies stored in a SQL Server database.

Its companion front-end, **[MovieCatalogUI](https://github.com/FarahOUERTANI/MovieCatalogUI)**, calls this API and displays the movies in a web page.

```
┌──────────────────┐   HTTP / JSON    ┌──────────────────┐    EF Core    ┌──────────────┐
│  MovieCatalogUI  │ ───────────────▶ │ MovieCatalogApi  │ ────────────▶ │  SQL Server  │
│   (ASP.NET MVC)  │ ◀─────────────── │  (REST API)      │ ◀──────────── │ MovieCatalog │
└──────────────────┘                  └──────────────────┘               └──────────────┘
```

## ✨ Features

- Full **CRUD** on movies
- **Code-first** database with EF Core migrations
- **Swagger UI** to explore and test the API from the browser
- Standard HTTP status codes (`200`, `201 Created`, `204 No Content`, `400`, `404`)
- Clean layering: Controllers / Models / Data (DbContext)

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Framework | ASP.NET Core 8 Web API |
| ORM | Entity Framework Core 9 (SQL Server) |
| Database | SQL Server LocalDB |
| Docs | Swashbuckle (Swagger / OpenAPI) |

## 🗂️ Project Structure

```
MovieCatalogApi/
├── Controllers/
│   └── MoviesController.cs    # REST endpoints /api/Movies
├── Data/
│   └── AppDbContext.cs        # EF Core DbContext
├── Migrations/                # InitialCreate migration
├── Models/
│   └── Movie.cs               # Movie entity
├── appsettings.json           # Connection string
└── Program.cs                 # Controllers, Swagger, DbContext
```

## 🧩 Data Model — `Movie`

| Field | Type | Description |
|---|---|---|
| `Id` | int | Primary key |
| `Title` | string | Movie title |
| `Description` | string | Short synopsis |
| `ReleaseDate` | DateOnly | Release date |
| `Genre` | string | Genre (e.g. Drama, Sci-Fi) |
| `Director` | string | Director's name |

## 🔌 API Endpoints

Base URL: `https://localhost:7240/api/Movies`

| Method | Endpoint | Description | Success response |
|---|---|---|---|
| `GET` | `/api/Movies` | Get all movies | `200 OK` + list |
| `GET` | `/api/Movies/{id}` | Get one movie | `200 OK` / `404` |
| `POST` | `/api/Movies` | Create a movie | `201 Created` |
| `PUT` | `/api/Movies/{id}` | Update a movie | `204 No Content` / `400` / `404` |
| `DELETE` | `/api/Movies/{id}` | Delete a movie | `204 No Content` / `404` |

### Example — create a movie

```http
POST /api/Movies
Content-Type: application/json

{
  "title": "Inception",
  "description": "A thief who steals secrets through dreams.",
  "releaseDate": "2010-07-16",
  "genre": "Sci-Fi",
  "director": "Christopher Nolan"
}
```

## 🚀 Getting Started

### Prerequisites
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- SQL Server LocalDB (or another SQL Server instance)
- EF Core CLI: `dotnet tool install --global dotnet-ef`

### Run it
1. Clone the repository:
   ```bash
   git clone https://github.com/FarahOUERTANI/MovieCatalogApi.git
   cd MovieCatalogApi/MovieCatalogApi
   ```
2. Check the connection string in `appsettings.json` (default: `MovieCatalogDb` on LocalDB).
3. Create the database:
   ```bash
   dotnet ef database update
   ```
4. Start the API with the HTTPS profile, which is the port MovieCatalogUI expects:
   ```bash
   dotnet run --launch-profile https
   ```
5. Open **https://localhost:7240/swagger** to try the endpoints.

## 🔮 Possible Improvements
- Validation attributes (`[Required]`, `[StringLength]`) on `Movie`
- DTOs to separate the API contract from the database entity
- Search and filter by genre or director
- Enable CORS if a JavaScript front-end needs to call the API

## 👩‍💻 Author

**Farah Ouertani** – [github.com/FarahOUERTANI](https://github.com/FarahOUERTANI)
