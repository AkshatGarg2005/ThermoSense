# **ThermoSense** 🌡⚡  
**Cross-Platform Real-Time Battery & Thermal Health Dashboard**  

ThermoSense combines **FastAPI**, **Machine Learning**, and a **React** frontend to monitor battery health and thermal stats in real time.  
Runs natively on macOS/Windows with a Dockerized frontend.  

---

## **📌 Features**
- 🔥 **Real-Time Monitoring** of battery temperature, thermal pressure, and CPU temperature (when supported).
- 🤖 **Random Forest Model** to predict health metrics.
- 🌐 **Cross-Platform** support for macOS (Intel/Apple Silicon) & Windows.
- 🐳 **Dockerized Frontend** for consistent deployment.
- 📊 **Interactive Charts & History Panel** for trend analysis.
- 🤝 **AI Advisory** powered by Gemini API.

---

## **📂 Directory Structure**
```

ThermoSense/
├── backend/                 # FastAPI backend + ML model + sensor scripts
│   ├── app.py                # FastAPI app entry
│   ├── main.py               # Alternative entry / setup
│   ├── system\_stats.py       # Hardware data collection
│   ├── gemini\_advisor.py     # AI-based advisory module
│   ├── requirements.txt      # Python dependencies
│   ├── thermosense\_test\_data.csv
│   ├── .env                  # API keys & secrets (ignored by Git)
│   └── Dockerfile            # Backend Dockerfile
│
└── docker/
├── client/               # React frontend + Nginx
│   ├── src/components/   # UI components
│   │   ├── Dashboard.jsx
│   │   ├── DualAxisChart.js
│   │   ├── HistoryPanel.jsx
│   │   ├── StatCard.jsx
│   │   └── TemperatureForm.js
│   ├── App.js
│   ├── Dockerfile
│   ├── nginx.conf
│   ├── package.json
│   └── ...
└── docker-compose.yml    # Orchestrates frontend container

````

---

## **🔑 Environment Variables**
Create a `backend/.env` file (**do not commit this to GitHub**):  
```env
OPENWEATHER_API_KEY=your_openweather_api_key_here
GEMINI_API_KEY=your_gemini_api_key_here
````

* `OPENWEATHER_API_KEY` → Fetches real-time weather data for context in predictions.
* `GEMINI_API_KEY` → Used for AI-powered advisory features (`gemini_advisor.py`).

---

## **🛠 First-Time Setup**

### **macOS**

```bash
git clone https://github.com/<your-username>/ThermoSense.git
cd ThermoSense

# Backend
python3 -m venv backend/.venv
source backend/.venv/bin/activate
pip install --upgrade pip
pip install -r backend/requirements.txt

# Frontend (Docker)
cd docker
docker compose build
```

### **Windows**

```powershell
git clone https://github.com/<your-username>/ThermoSense.git
cd ThermoSense

# Backend
python -m venv backend\.venv
.\backend\.venv\Scripts\Activate.ps1
pip install --upgrade pip
pip install -r backend\requirements.txt
pip install wmi   # Optional CPU temp

# Frontend (Docker)
cd docker
docker compose build
```

---

## **🚀 Running the App**

**1️⃣ Start FastAPI Backend**

* **macOS**

```bash
cd backend
source .venv/bin/activate
sudo uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

* **Windows**

```powershell
cd backend
.\.venv\Scripts\Activate.ps1
uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

**2️⃣ Start React Frontend**

```bash
cd docker
docker compose up -d
```

**3️⃣ Open in Browser**

```
http://localhost:3000
```

---

## **🛑 Stopping the App**

```bash
# Stop backend: Ctrl + C
# Stop frontend:
cd docker
docker compose down
```

---

## **📌 Notes**

* macOS requires `sudo` for `powermetrics` (consider adding to `/etc/sudoers` for passwordless use).
* Windows temperature monitoring depends on motherboard sensor availability via WMI.
* `docker-compose.yml` sets `REACT_APP_API_ROOT` for frontend-backend communication.


