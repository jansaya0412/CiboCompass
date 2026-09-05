# CiboCompass 🍝🧭

CiboCompass is a mobile app that helps international students in Italy navigate local cuisine with confidence — combining ingredient transparency, dietary filtering, and culturally-aware peer reviews to answer three simple questions:

- **What's this dish? Can I eat it?**
- **What do I think about it afterward?**
- **Do people like this in my culture?**

## Demo

![Demo](demo.gif)

## The Problem

International students in Italy often struggle with unfamiliar menus, unclear ingredients, and dietary uncertainty (halal, vegetarian, allergens, etc.). Existing tools like Google Translate, MyFitnessPal, or Google Maps handle pieces of this problem, but none combine translation, cultural sensitivity, ingredient transparency, and personalized feedback in one place.

## Research Behind the App

CiboCompass was grounded in real user research, not just assumptions:

- **20 structured interviews** with international students across cultural and dietary backgrounds
- **170+ survey responses** (140 valid after cleaning), which showed:
  - 40%+ rated ingredient lists as the most useful feature
  - ~70% wanted peer reviews from users with similar backgrounds
  - Strong demand for dietary filters (halal, vegan, allergens)
- **Competitor analysis** of MyFitnessPal, Lifesum, Google Maps, Instagram, Xiaohongshu, and HappyCow
- **Paper prototyping** with 5 participants, followed by iterative **Figma prototyping** validated through expert cognitive walkthroughs

Full methodology, data, and findings are documented in [`Final_report.pdf`](./Final_report.pdf).

## Features

- 🔍 Real-time dish search with ingredient breakdowns (tabular format)
- 🏷️ Dietary badges — automatically flags Vegetarian, Vegan, Halal, Kosher, and Gluten-Free dishes based on ingredient analysis
- ⭐ Five-star rating system with interactive feedback
- 🌍 Culturally filtered ratings — see how people from your background rated a dish
- 📱 Native iOS-inspired design (large titles, segmented controls) built with a single cross-platform codebase

## Project Structure

```
CiboCompass/
├── cmd-api/            # Go API server
│   ├── main.go         # Entry point
│   ├── routes.go       # Route definitions
│   ├── dishes.go       # Dish endpoint handlers
│   ├── errors.go       # Error handling helpers
│   ├── healthcheck.go  # Health check endpoint
│   ├── helpers.go      # Shared helper functions
│   └── *_test.go       # Tests
├── databases/          # Database layer
│   ├── database.go     # DB connection/setup
│   ├── dishes.go       # Dish data access
│   └── database_test.go
├── Final_report.pdf    # Full project report (research, design, dev process)
├── demo.gif            # App demo preview
└── .gitignore
```

## Tech Stack

**Backend**
- Go
- `httprouter` for routing
- SQLite (`mattn/go-sqlite3`)

**Frontend**
- React Native (Expo SDK 53, React 19)
- AsyncStorage for local persistence
- iOS and Android support

**API Routes**
| Method | Endpoint | Description |
|--------|----------|--------------|
| GET | `/v1/dishes/{name}` | Fetch dish details |
| POST | `/v1/dishes/{name}/feedback` | Submit user feedback |
| GET | `/v1/healthcheck` | Server status check |

The backend personalizes responses using a nationality header, returning culturally relevant feedback per dish.

## Database Schema

- **Dishes** – core dish data, images, descriptions
- **Ingredients** – standardized ingredient list
- **DishesToIngredients** – many-to-many mapping
- **Feedbacks** – user ratings, filtered by nationality

## Getting Started

### Backend
```bash
cd cmd-api
go run main.go
# Server runs on http://localhost:4000
```

### Frontend
The React Native frontend lives in a separate repo/folder — see project links in `Final_report.pdf` for details.

## Usability Testing Highlights

- Small-scale usability tests (5–7 participants) validated the React Native build with no crashes or functional issues
- Users responded well to the culturally filtered ratings and dietary tag system
- Iterative feedback led to a five-star rating system (replacing an earlier thumbs up/down), a tabular ingredient layout, and text-based allergen tags (replacing emojis)

## Roadmap

- [ ] Recent searches
- [ ] Display number of ratings per dish
- [ ] Comment section for qualitative feedback
- [ ] Persistent user sessions
- [ ] Search filtering options
- [ ] Dish categories and drinks menu

## Team

A team of six international students studying in Italy, building CiboCompass out of firsthand experience navigating Italian menus.

## Acknowledgements

AI tools were used throughout the project — for report drafting, persona generation, survey design, storyboard illustration, and debugging — with each use documented transparently in `Final_report.pdf`.
