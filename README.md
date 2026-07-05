# YouTube Tools

A Spring Boot web application providing utilities for YouTube content creators — extract high-resolution thumbnails, generate SEO tag suggestions, and view video metadata.

Built with **Spring Boot**, **Thymeleaf**, and the **YouTube Data API v3**, following a classic MVC architecture.

---

## Features

| Feature | Status | Description |
|---|---|---|
| 🖼️ Thumbnail Generator | ✅ Working | Extracts a video ID from any YouTube URL format and generates a direct high-res thumbnail link, downloadable in one click. |
| 🏷️ SEO Tag Generator | 🚧 In progress | UI and data models are complete; integration with the YouTube Data API's search/videos endpoints is the current focus. |
| 📊 Video Metadata Viewer | 🚧 In progress | Template built; controller wiring in progress. |

---

## Tech Stack

- **Java 21**
- **Spring Boot 3.5.5** (Spring MVC)
- **Thymeleaf** — server-side templating
- **Spring WebFlux `WebClient`** — for calling the YouTube Data API v3
- **Lombok** — reduces model boilerplate
- **Maven** — build and dependency management
- **Tailwind CSS** + Bootstrap Icons — frontend styling
- **Docker** — containerized build and run

---

## Architecture

```
Browser → Controller (@Controller) → Service (@Service) → Model → Thymeleaf View → Browser
```

Standard Spring MVC request flow: controllers handle HTTP requests and delegate business logic (URL parsing, YouTube API calls) to service classes, then populate a `Model` that Thymeleaf renders into HTML server-side.

---

## Getting Started

### Prerequisites
- JDK 21+
- Maven (or use the included `mvnw` wrapper — no local Maven install needed)
- A [YouTube Data API v3](https://console.cloud.google.com/apis/library/youtube.googleapis.com) key

### 1. Clone the repo
```bash
git clone https://github.com/<your-username>/YouTubeTools.git
cd YouTubeTools
```

### 2. Configure your API key
This project reads the API key from an environment variable — **never commit a real key**.

Set it in your shell:
```bash
export YOUTUBE_API_KEY=your_api_key_here      # macOS/Linux
setx YOUTUBE_API_KEY "your_api_key_here"      # Windows
```

See `application.properties.example` for the full list of configurable properties.

### 3. Run locally
```bash
./mvnw spring-boot:run
```
The app will start on **http://localhost:8080**.

---

## Running with Docker

Build the image:
```bash
docker build -t youtube-tools .
```

Run the container, passing your API key at runtime:
```bash
docker run -p 8080:8080 -e YOUTUBE_API_KEY=your_api_key_here youtube-tools
```

Visit **http://localhost:8080**.

---

## Project Structure

```
src/main/java/com/YouTubeTools/
├── controller/       # Handles HTTP requests, returns view names
├── service/          # Business logic (URL parsing, API calls)
└── model/            # Data classes (Video, SearchVideo)

src/main/resources/
├── templates/        # Thymeleaf HTML views
└── application.properties
```

---

## Roadmap

- [ ] Finish `YouTubeService` integration with the YouTube Data API `/search` and `/videos` endpoints
- [ ] Wire up the video metadata controller
- [ ] Add unit tests for URL-parsing logic and `@WebMvcTest` coverage for controllers
- [ ] Add response caching to reduce YouTube API quota usage
- [ ] Basic rate limiting on public-facing endpoints

---

## License

This project is for educational/portfolio purposes.
