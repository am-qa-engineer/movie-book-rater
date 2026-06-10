# 🎬 CineShelf — Movie & Book Rating App

![QA Pipeline](https://github.com/YOUR_USERNAME/movie-book-rater/actions/workflows/qa-pipeline.yml/badge.svg)
![Data Valid](https://img.shields.io/badge/Data-JSON%20on%20GitHub-gold)
![Selenium](https://img.shields.io/badge/Tests-Selenium%20%2B%20TestNG-green)
![Live Demo](https://img.shields.io/badge/Live-GitHub%20Pages-blue)

> **A full-stack QA showcase project.** A live movie & book rating web app — with Selenium UI automation, GitHub API testing, JSON cloud storage, and a complete CI/CD pipeline. Built to demonstrate end-to-end QA engineering skills.

**🌐 Live Demo:** [YOUR_USERNAME.github.io/movie-book-rater/app](https://YOUR_USERNAME.github.io/movie-book-rater/app)

---

## 🏗️ What Makes This Interesting

| Feature | Why It's Clever |
|---------|----------------|
| **GitHub as Cloud Storage** | `data/ratings.json` is the database. Every rating is a real Git commit — full audit trail, zero infra cost |
| **Live + Testable** | Deployed on GitHub Pages — Selenium tests run against the real live URL |
| **API Testing the Storage** | Tests validate the GitHub Contents API that serves the JSON — tests the cloud layer itself |
| **Auto-deploy on passing tests** | CI only deploys to GitHub Pages if all tests pass first |
| **Data validation in CI** | Python script validates `ratings.json` schema on every push |

---

## 📁 Project Structure

```
movie-book-rater/
├── app/
│   └── index.html              # The full single-file web app
├── data/
│   └── ratings.json            # ☁️ Cloud storage — all ratings live here
├── tests/
│   ├── selenium/               # UI automation — Java + Selenium + TestNG
│   │   └── src/test/java/
│   │       └── tests/CineShelfUITest.java   # 13 UI test cases
│   ├── api/                    # API automation — Java + RestAssured
│   │   └── src/test/java/
│   │       └── tests/GitHubStorageAPITest.java  # 10 API test cases
│   └── manual/
│       └── Test_Cases.xlsx     # Manual test cases + bug report
├── .github/workflows/
│   └── qa-pipeline.yml         # Full CI/CD pipeline
└── docs/
    └── test-plan.md
```

---

## ✅ Test Coverage

### UI Tests — Selenium + TestNG (13 tests)
| TC ID | Test Scenario | Group |
|-------|-------------|-------|
| TC_UI_01 | Page title contains "CineShelf" | Smoke |
| TC_UI_02 | Hero heading visible on load | Smoke |
| TC_UI_03 | All 4 tab buttons present | Smoke |
| TC_UI_04 | Rating form visible | Smoke |
| TC_UI_05 | Submit without title shows toast error | Regression |
| TC_UI_06 | Submit without star rating shows toast error | Regression |
| TC_UI_07 | Valid submission shows success toast | Regression |
| TC_UI_08 | Movie type button active by default | Regression |
| TC_UI_09 | Book type toggle works correctly | Regression |
| TC_UI_10 | Movies tab filters to movies only | Regression |
| TC_UI_11 | Books tab filters to books only | Regression |
| TC_UI_12 | Responsive layout at 375px mobile width | Regression |
| TC_UI_13 | Stats section loads real values | Regression |

### API Tests — RestAssured (10 tests)
| TC ID | Test Scenario |
|-------|-------------|
| TC_API_01 | GitHub API is reachable |
| TC_API_02 | Repository exists and is accessible |
| TC_API_03 | ratings.json file exists in repo |
| TC_API_04 | File decodes as valid JSON |
| TC_API_05 | Ratings array is not empty |
| TC_API_06 | Each rating has all required fields |
| TC_API_07 | Rating values are between 1 and 5 |
| TC_API_08 | Type field is "movie" or "book" only |
| TC_API_09 | Date is valid ISO format (YYYY-MM-DD) |
| TC_API_10 | All rating IDs are unique |

---

## ⚙️ CI/CD Pipeline

```
Push to main
      │
      ▼
┌──────────────────┐
│ Validate JSON    │  Python schema validation
└────────┬─────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌────────┐  ┌──────────┐
│  API   │  │    UI    │  ← Parallel
│ Tests  │  │  Tests   │
└───┬────┘  └────┬─────┘
    └──────┬─────┘
           ▼
    ┌──────────────┐
    │    Deploy    │  GitHub Pages — only if ALL tests pass
    └──────────────┘
```

**Triggers:** Push to main, Pull Requests, Nightly at 3AM UTC, Manual dispatch

---

## ☁️ How GitHub Storage Works

```javascript
// Each rating is saved as a commit to ratings.json via GitHub API
const payload = {
  message: `Add rating: ${title} — ${rating}★`,
  content: btoa(JSON.stringify(updatedData)),
  sha:     currentFileSHA   // required to update the file
};

await fetch('https://api.github.com/repos/USER/REPO/contents/data/ratings.json', {
  method: 'PUT',
  headers: { 'Authorization': `token ${PAT}` },
  body: JSON.stringify(payload)
});
```

Every submitted rating creates a **real Git commit** — giving you a complete, auditable history of all ratings. No database, no server, no cost.

---

## 🚀 Setup & Run

### View the live app
Visit: `https://YOUR_USERNAME.github.io/movie-book-rater/app`

### Enable write access (submit ratings)
1. Generate a GitHub Personal Access Token (PAT) with `repo` scope
2. Open `app/index.html` and set `GITHUB_TOKEN = 'your_pat_here'`
3. Set `GITHUB_USER = 'your_username'`

### Run UI tests locally
```bash
cd tests/selenium
mvn test -Dapp.url=https://YOUR_USERNAME.github.io/movie-book-rater/app/ -Dheadless=false
```

### Run API tests locally
```bash
cd tests/api
mvn test -Dgithub.user=YOUR_USERNAME
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | HTML5, CSS3, Vanilla JavaScript |
| Cloud Storage | GitHub Contents API + JSON |
| Deployment | GitHub Pages |
| UI Tests | Java 11, Selenium 4, TestNG |
| API Tests | Java 11, RestAssured, TestNG |
| CI/CD | GitHub Actions |
| Data Validation | Python 3 |

---

## 🔮 Planned Additions

- [ ] Search and filter ratings by title
- [ ] User authentication via GitHub OAuth
- [ ] Performance tests with JMeter
- [ ] Docker-based test environment
- [ ] Playwright tests alongside Selenium

---

## 👤 Author

**[Your Name]** — QA Engineer  
[LinkedIn](https://linkedin.com/in/YOUR_LINKEDIN) • [GitHub](https://github.com/YOUR_USERNAME)
