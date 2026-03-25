***

# 🌾 CropDoc: AI-Powered Crop Health Monitor

[cite_start]**Aharada Kaushal Kumbh 2026 Hackathon Submission** [cite: 6]
[cite_start]**Track:** Smart Agriculture [cite: 7]
[cite_start]**Developer:** Solo Submission [cite: 9]

[cite_start]CropDoc is a mobile-first web application designed to put expert agronomist knowledge directly into the hands of farmers[cite: 11]. [cite_start]By leveraging edge-friendly Machine Learning, real-time weather data, and Generative AI, CropDoc identifies plant diseases, predicts yield impacts, and provides hyper-localized, weather-aware treatment plans in vernacular languages[cite: 12, 13, 14].

[cite_start]This project directly addresses the hackathon problem statement: *"Leverage IoT and ML to monitor crop health, predict yields, and optimize resource usage."* [cite: 8]

---

## ✨ Core Features

* [cite_start]**Instant Disease Identification:** Fast image classification using a lightweight MobileNetV2 model fine-tuned on the "New Plant Diseases Dataset" (87K+ images across 38 classes)[cite: 16, 36, 41].
* [cite_start]**Resource Optimization (Weather-Aware AI):** Integrates with the Open-Meteo API to check hyper-local 7-day weather forecasts[cite: 17, 38]. [cite_start]The AI prevents resource waste (e.g., advising against chemical sprays if rain is imminent)[cite: 18].
* [cite_start]**Yield Impact Estimator:** Calculates potential crop loss based on disease severity and user-inputted farm size[cite: 19].
* [cite_start]**Vernacular / Multi-language UI:** Simple toggle to switch AI output between English and local languages (e.g., Hindi) for real-world accessibility[cite: 20].
* [cite_start]**Mobile-First Interface:** Responsive UI optimized for field devices with low bandwidth[cite: 21].

---

## 🛠️ Technology Stack

[cite_start]**Frontend (User Interface)** [cite: 23]
* [cite_start]**Framework:** Vite + React [cite: 108] [cite_start](Note: Architecture originally considered HTML+Vanilla JS [cite: 24]).
* [cite_start]**Styling:** Tailwind CSS [cite: 25, 108]
* [cite_start]**Hosting:** Vercel [cite: 30, 112]

[cite_start]**Backend (API & ML Serving)** [cite: 31]
* [cite_start]**Framework:** FastAPI (Python) for asynchronous support[cite: 32].
* [cite_start]**Hosting:** Render or Railway[cite: 34].

[cite_start]**Machine Learning & External APIs** [cite: 35]
* [cite_start]**Classification Model:** MobileNetV2 (TensorFlow/Keras)[cite: 36].
* [cite_start]**Generative AI:** Google Gemini API[cite: 37].
* [cite_start]**Weather Data:** Open-Meteo API[cite: 38].

---

## ⚙️ System Architecture & Data Flow

1.  [cite_start]**Client Interaction:** The farmer uploads a leaf image, inputs farm size (acres/hectares), and grants browser GPS permission via the React frontend[cite: 43, 44].
2.  [cite_start]**Data Transmission:** Image, GPS coordinates, and farm size are sent as a `multipart/form-data` payload via a POST request to the FastAPI backend[cite: 45].
3.  **Parallel Processing:**
    * [cite_start]*ML Inference:* The Python backend resizes the image to 224x224, and the `.h5` model predicts the disease class[cite: 46].
    * [cite_start]*Weather Fetch:* The backend pings the Open-Meteo API using GPS coordinates to fetch 48-hour precipitation and temperature data[cite: 47].
4.  [cite_start]**GenAI Enrichment:** The predicted disease, weather data, and farm size are injected into a dynamic Google Gemini prompt to generate a 3-step organic treatment plan and a yield loss estimate[cite: 48].
5.  [cite_start]**Response Formulation:** FastAPI bundles the data into a JSON object[cite: 49].
6.  [cite_start]**Client Display:** The React frontend renders the comprehensive results dashboard to the farmer[cite: 50].

---

## 📡 API Interface Specification

[cite_start]**Endpoint:** `/api/predict` [cite: 56]
[cite_start]**Method:** `POST` [cite: 57]
[cite_start]**Content-Type:** `multipart/form-data` [cite: 58]
[cite_start]**Payload:** `file` (Image), `latitude` (Float), `longitude` (Float), `farm_size` (Float), `language` (String: "en" or "hi") [cite: 59, 60]

[cite_start]**Success Response (200 OK):** [cite: 61]
```json
{
  "status": "success",
  "data": {
    "crop": "Tomato",
    "disease": "Early Blight",
    "confidence_score": 0.965,
    "weather_context": "Heavy rain expected in 4 hours.",
    "yield_impact_estimate": "Potential 20-30% yield loss if left untreated.",
    "treatment_plan": "1. Remove and destroy lower infected leaves immediately..."
  }
}
```

---

## 🚀 Getting Started (Local Development)

*(Instructions to be added once repository folders are initialized)*
1. Clone the repository.
2. Navigate to the `/backend` folder, install Python requirements (`pip install -r requirements.txt`), and run the FastAPI server.
3. Navigate to the `/frontend` folder, install Node dependencies (`npm install`), and run the Vite development server (`npm run dev`).
4. Ensure you have your `GEMINI_API_KEY` configured in your backend `.env` file.

***

Would you like me to generate the foundational FastAPI backend code to get the `/api/predict` endpoint up and running?
