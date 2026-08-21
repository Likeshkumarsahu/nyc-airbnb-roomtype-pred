# 🏙️ NYC Airbnb Room Type Predictor

> A full-stack machine learning application that predicts whether an NYC Airbnb listing is an **Entire home/apt**, **Private room**, or **Shared room** — powered by a scikit-learn pipeline served through a FastAPI backend and a polished vanilla-JS frontend.

---

## 📸 Preview

<!-- Add a screenshot of the app here once deployed -->
<!-- ![App Preview](./preview.png) -->

---

## ✨ Features

- **ML-powered predictions** — Classifies NYC Airbnb listings into 3 room types with probability scores
- **Interactive UI** — Animated NYC skyline, building visualisations that scale with confidence, and smooth count-up animations
- **One-click examples** — Cycle through realistic pre-filled listing examples (Manhattan, Brooklyn, Queens)
- **Live API health check** — Real-time indicator showing whether the backend is reachable
- **Input validation** — Pydantic-enforced schema validation on the backend, HTML5 constraint validation on the frontend
- **Responsive design** — Works across desktop and mobile screen sizes
- **Accessibility-first** — ARIA labels, `role="alert"` for results, and `prefers-reduced-motion` support

---

## 🗂️ Project Structure

```
NYC-Airbnb-Room-Type-Predictor-main/
├── main.py                              # FastAPI application & /predict endpoint
├── Model_Pipeline.pkl                   # Pre-trained scikit-learn pipeline (~36 MB)
├── nyc_airbnb_room_type_classification.ipynb  # EDA, feature engineering & model training notebook
├── index.html                           # Frontend UI (vanilla HTML)
├── style.css                            # Styling (Space Grotesk, dark theme, animations)
├── script.js                            # Frontend logic (form wiring, API calls, result rendering)
├── requirements.txt                     # Python dependencies
└── nyc-ml/                              # Python virtual environment (local)
```

---

## 🧠 Model

The ML pipeline (`Model_Pipeline.pkl`) was trained on the [NYC Airbnb Open Data](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data) dataset and built in the accompanying Jupyter Notebook.

### Input Features

| Feature | Type | Description |
|---|---|---|
| `latitude` | `float` | Listing latitude (−90 to 90) |
| `longitude` | `float` | Listing longitude (−180 to 180) |
| `price` | `float` | Price per night in USD (> 0) |
| `minimum_nights` | `int` | Minimum nights required (1 – 365) |
| `number_of_reviews` | `int` | Total number of reviews (≥ 0) |
| `reviews_per_month` | `float` | Average reviews per month (≥ 0) |
| `calculated_host_listings_count` | `int` | Total listings by the host (≥ 0) |
| `availability_365` | `int` | Days available per year (0 – 365) |
| `neighbourhood_group` | `str` | NYC Borough (e.g. Manhattan, Brooklyn) |
| `neighbourhood` | `str` | Specific neighbourhood name |

### Output Classes

| Class | Description |
|---|---|
| `Entire home/apt` | The whole property is reserved exclusively for guests |
| `Private room` | A private room within a shared property |
| `Shared room` | A shared sleeping space with other guests |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- A virtual environment tool (e.g. `venv`)

### 1. Clone the repository

```bash
git clone https://github.com/your-username/NYC-Airbnb-Room-Type-Predictor.git
cd NYC-Airbnb-Room-Type-Predictor
```

### 2. Create and activate a virtual environment

```bash
python -m venv venv
source venv/bin/activate        # Linux / macOS
# venv\Scripts\activate         # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Start the FastAPI server

```bash
uvicorn main:app --reload
```

The API will be available at `http://127.0.0.1:8000`.

### 5. Open the frontend

Simply open `index.html` in your browser, or serve it with any static file server:

```bash
# Using Python's built-in server
python -m http.server 3000
```

Then visit `http://localhost:3000`.

> **Note:** If you're running the backend locally, update `API_BASE_URL` in `script.js` to point to `http://127.0.0.1:8000`.

---

## 🌐 API Reference

The backend exposes two endpoints:

### `GET /`
Health check — returns a greeting string confirming the server is running.

### `POST /predict`

**Request Body** (JSON):

```json
{
  "latitude": 40.7484,
  "longitude": -73.9857,
  "price": 120,
  "minimum_nights": 2,
  "number_of_reviews": 84,
  "reviews_per_month": 2.3,
  "calculated_host_listings_count": 1,
  "availability_365": 210,
  "neighbourhood_group": "Manhattan",
  "neighbourhood": "Midtown"
}
```

**Response** (JSON):

```json
{
  "Predicted_room_type": "Entire home/apt",
  "Probability": [0.87, 0.11, 0.02]
}
```

The `Probability` array is aligned to the model's `classes_` order: `["Entire home/apt", "Private room", "Shared room"]`.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **ML / Data** | scikit-learn, pandas, NumPy, Matplotlib, Seaborn |
| **Backend** | FastAPI, Uvicorn, Pydantic, Joblib |
| **Frontend** | Vanilla HTML5, CSS3, JavaScript (ES2022) |
| **Fonts** | Space Grotesk, Inter, JetBrains Mono (Google Fonts) |
| **Deployment** | [Render](https://render.com) (backend API) |

---

## ☁️ Deployment

The FastAPI backend is deployed on **Render** at:

```
https://nyc-airbnb-room-type-predictor.onrender.com
```

The frontend (`index.html`) can be hosted on any static hosting service — GitHub Pages, Netlify, Vercel, etc.

---

## 📓 Notebook

The Jupyter Notebook `nyc_airbnb_room_type_classification.ipynb` covers the full ML workflow:

1. **Data loading & exploration** — Understanding the raw NYC Airbnb dataset
2. **Exploratory Data Analysis (EDA)** — Distributions, correlations, borough breakdowns
3. **Feature engineering** — Encoding categorical columns, handling missing values
4. **Model training** — Training and comparing multiple classifiers
5. **Pipeline construction** — Wrapping preprocessing + model into a single `sklearn.Pipeline`
6. **Evaluation** — Accuracy, classification report, confusion matrix
7. **Export** — Saving the final pipeline as `Model_Pipeline.pkl` with `joblib`

---

## 📋 Requirements

```
fastapi==0.115.6
uvicorn[standard]==0.34.0
pydantic==2.10.4
pandas==2.2.3
scikit-learn==1.6.1
joblib==1.4.2
numpy
matplotlib
seaborn
ipykernel
```

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 🙏 Acknowledgements

- [NYC Airbnb Open Data](https://www.kaggle.com/datasets/dgomonov/new-york-city-airbnb-open-data) — Dataset used for training
- [FastAPI](https://fastapi.tiangolo.com/) — High-performance Python web framework
- [scikit-learn](https://scikit-learn.org/) — ML pipeline and classifiers
- [Render](https://render.com) — Free-tier cloud deployment

---

<p align="center">Made with ❤️ for NYC listings data</p>
