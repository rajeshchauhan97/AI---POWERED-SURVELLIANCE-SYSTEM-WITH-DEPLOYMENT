***AI-Powered Surveillance System*** 🔍

YOLOv8 + DeepSORT + Flask + Docker + AWS EC2 + NVIDIA GPU

A real-time AI surveillance system for detecting objects, weapons, and zone intrusions, with instant alerts via email/SMS. Built with Flask, OpenCV, YOLOv8, DeepSORT, and Docker — deployed on AWS EC2 with GPU acceleration.

📌 Features
Real-time object & weapon detection (YOLOv8)

Person tracking (DeepSORT)

Restricted zone intrusion detection

Email and SMS alerts with image snapshots

Flask-based live video streaming UI

GPU-accelerated Docker deployment

Cloud deployment on AWS EC2 with NVIDIA GPU

🧠 Technologies Used
YOLOv8 (Ultralytics)

DeepSORT for multi-object tracking

Flask (Web framework)

OpenCV (Live video processing)

Docker + NVIDIA Container Toolkit

AWS EC2 (Ubuntu with NVIDIA GPU)

Twilio (SMS & email notifications)

⚙️ Setup Instructions (From VENV to Deployment)
1. Clone the Repository
git clone https://github.com/your-username/ai-surveillance-system.git
cd ai-surveillance-system

2. Create & Activate Virtual Environment
python -m venv venv
source venv/bin/activate    # On Windows: venv\Scripts\activate

3. Install Requirements
pip install -r requirements.txt

Important Note on Dependencies:
This project uses specific versions of libraries to ensure compatibility, especially for GPU acceleration. The requirements.txt file pins these versions:

# AI/ML Core
torch==2.1.0
torchvision==0.16.0
torchaudio==2.1.0
ultralytics==8.0.203
deep-sort-realtime==1.2.0

# Flask and Web
flask==2.3.3
gunicorn==22.0.0
python-dotenv==1.0.0

# CV + Utils
opencv-python==4.9.0.80
numpy==1.23.5
Pillow==10.3.0
matplotlib==3.8.4

# Alerts
twilio==8.10.1
email-validator==2.1.0.post1
requests==2.32.3
pygame==2.5.2

Ensure app/track.py has embedder_gpu=True enabled in the DeepSORTTracker initialization for GPU acceleration.

4. Run Locally (For Testing)
python app/main.py

Open your browser and navigate to: http://localhost:5000

🐳 Docker Deployment
1. Build Docker Image
docker build -t ai-surveillance .

2. Run Container with GPU
docker run --gpus all -p 5000:5000 ai-surveillance

Open your browser and navigate to: http://localhost:5000

☁️ AWS EC2 Deployment (GPU)
Launch an Ubuntu EC2 instance with an NVIDIA GPU (e.g., g4dn.xlarge).

SSH into your instance:

ssh -i "your-key.pem" ubuntu@your-ec2-ip

Install NVIDIA drivers & Docker with GPU support:

# Install NVIDIA drivers (version may vary, check NVIDIA's site for latest compatible with your instance)
sudo apt update && sudo apt install -y nvidia-driver-525 

# Install Docker
curl -fsSL https://get.docker.com | sh

# Install NVIDIA Container Toolkit
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) && \
curl -s -L https://nvidia.github.io/libnvidia-container/gpgkey | sudo apt-key add - && \
curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | sudo tee /etc/apt/sources.list.d/libnvidia-container.list && \
sudo apt-get update && sudo apt-get install -y nvidia-docker2
sudo systemctl restart docker

Clone repo and run Docker:

git clone https://github.com/your-username/ai-surveillance-system.git
cd ai-surveillance-system/Docker # Navigate to the Docker directory
sudo docker-compose -f compose.yml up --build -d # Use docker-compose for easier management

Note: Ensure your docker-compose.yml includes runtime: nvidia under the service definition for GPU access. Also, update ../.env with your Twilio/email credentials.

Now open your browser and navigate to: http://<your-ec2-ip>

📦 Folder Structure
AI_Surveillance_System/
│
├── app/
│   ├── main.py
│   ├── video_feed.py
│   ├── track.py
│   ├── alert.py
│   ├── utils.py
│
├── models/
│   └── yolov8n.pt 
│
├── static/
│   ├── alert_images/
│   └── sound_alerts/
│
├── templates/
│   └── index.html
│
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── README.md

📬 Alerts Example
Email/SMS sent with image, object type, timestamp

Triggered on weapon detection or zone violation

🤝 Contributing
Pull requests welcome! For major changes, open an issue first to discuss what you'd like to change.
