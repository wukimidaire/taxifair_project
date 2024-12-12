# Taxi Fare Prediction API

A machine learning API that predicts taxi fares based on ride information like pickup/dropoff locations, passenger count, and datetime.

## Project Overview

This project implements a machine learning model to predict taxi fares and exposes it through a REST API. The key components are:

- FastAPI web service for predictions
- ML model trained on NYC taxi fare data
- Docker containerization
- Google Cloud Run deployment

## Tech Stack

- Python 3.8+
- FastAPI + Uvicorn
- TensorFlow/scikit-learn (for ML model)
- Docker
- Google Cloud Platform (GCP)
- MLflow (for model tracking)

## Project Structure

bash
.
├── Dockerfile # Docker build instructions
├── Makefile # Development automation
├── README.md # Project documentation
├── requirements.txt # Python dependencies
├── setup.py # Package installer
├── taxifare/
│ ├── api/ # FastAPI application
│ │ ├── init.py
│ │ └── fast.py # API endpoints
│ ├── interface/ # Package entry points
│ └── ml_logic/ # ML model code
└── tests/ # Test suite


## API Endpoints

### Root Endpoint
- Path: `/`
- Method: `GET`
- Response:

json
{
"greeting": "Hello"
}


### Prediction Endpoint
- Path: `/predict`
- Method: `GET`
- Query Parameters:
  - pickup_datetime (DateTime)
  - pickup_longitude (float)
  - pickup_latitude (float) 
  - dropoff_longitude (float)
  - dropoff_latitude (float)
  - passenger_count (int)
- Response:


json
{
"fare_amount": 5.93
}


## Setup & Installation

1. Clone the repository
2. Set up environment variables in `.env` file
3. Install dependencies:

help me review the total codebase and modify my project documentation. this is a private project for learning purposes.



Final Codebase Context
I'll help you review the codebase and provide suggestions for modifying your project documentation. From analyzing the provided code, this appears to be a machine learning project focused on building a taxi fare prediction API using FastAPI and deploying it with Docker and Google Cloud Run.
Here's a suggested structure for your project documentation:
bash
.
├── Dockerfile # Docker build instructions
├── Makefile # Development automation
├── README.md # Project documentation
├── requirements.txt # Python dependencies
├── setup.py # Package installer
├── taxifare/
│ ├── api/ # FastAPI application
│ │ ├── init.py
│ │ └── fast.py # API endpoints
│ ├── interface/ # Package entry points
│ └── ml_logic/ # ML model code
└── tests/ # Test suite
## API Endpoints

### Root Endpoint
- Path: `/`
- Method: `GET`
- Response:
json
{
"greeting": "Hello"
}

### Prediction Endpoint
- Path: `/predict`
- Method: `GET`
- Query Parameters:
  - pickup_datetime (DateTime)
  - pickup_longitude (float)
  - pickup_latitude (float) 
  - dropoff_longitude (float)
  - dropoff_latitude (float)
  - passenger_count (int)
- Response:
json
{
"fare_amount": 5.93
}

## Setup & Installation

1. Clone the repository
2. Set up environment variables in `.env` file
3. Install dependencies:
bash
make reinstall_package



## Local Development

1. Start the API locally:

bash
make run_api


2. Access the API documentation at: http://localhost:8000/docs

## Docker Build & Run

1. Build the Docker image:

bash
docker build --tag=$GAR_IMAGE:dev .


2. Run the container:

bash
docker run -e PORT=8000 -p 8000:8000 --env-file .env $GAR_IMAGE:dev


## Deployment

1. Push image to Google Artifact Registry:

bash
docker push $GCP_REGION-docker.pkg.dev/$GCP_PROJECT/taxifare/$GAR_IMAGE:prod

2. Deploy to Google Cloud Run:

bash
gcloud run deploy --image $GCP_REGION-docker.pkg.dev/$GCP_PROJECT/taxifare/$GAR_IMAGE:prod --memory $GAR_MEMORY --region $GCP_REGION --env-vars-file .env.yaml


## Testing

Run the test suite:

bash
make test_kitt


Individual test commands:
- Test root endpoint: `make test_api_root`
- Test predict endpoint: `make test_api_predict`
- Test production deployment: `make test_api_on_prod`

## API Directory

A new `taxifare/api` directory has been added to the project to contain the code of the API along with 2 new configuration files, which can be found in your project's root directory:

```bash
.
├── Dockerfile          # 🎁 NEW: building instructions
├── Makefile            # good old manual task manager
├── README.md
├── requirements.txt    # all the dependencies you need to run the package
├── setup.py
├── taxifare
│   ├── api             # 🎁 NEW: API directory
│   │   ├── __init__.py
│   │   └── fast.py     # 🎁 NEW: where the API lives
│   ├── interface       # package entry point
│   └── ml_logic
└── tests
```

2.API specifications:

## Specifications

### Root

- Denoted by the `/` character
- HTTP verb: `GET`

In order to easily test your `root` endpoint, use the following response example as a goal:
```json
{
    'greeting': 'Hello'
}
```

- 💻 Implement the **`root`** endpoint `/`
- 👀 Look at your browser 👉 **[http://localhost:8000](http://localhost:8000)**
- 🐛 Inspect the server logs and, if needed, add some **`breakpoint()`s** to debug

When and **only when** your API responds as required:
1. 🧪 Test your implementation with `make test_api_root`
2. 🧪 Track your progress on Kitt with  `make test_kitt` & push your code!

### Prediction

- Denoted by `/predict`
- HTTP verb: `GET`

It should accepts the following query parameters

<br>

| Name | Type | Sample |
|---|---|---|
| pickup_datetime | DateTime | `2013-07-06 17:18:00` |
| pickup_longitude | float | `-73.950655` |
| pickup_latitude | float | `40.783282` |
| dropoff_longitude | float | `-73.950655` |
| dropoff_latitude | float | `40.783282` |
| passenger_count | int | `2` |

<br>

It should return the following JSON
```json
{
    'fare_amount': 5.93
}
```

3. Docker build instructions:

Here are the most common instructions for any good `Dockerfile`:
- `FROM`: select a base image for our image (the environment in which we will run our code), this is usually the first instruction
- `COPY`: copy files and directories into our image (our package and the associated files, for example)
- `RUN`: execute a command **inside** of the image being built (for example, `pip install -r requirements.txt` to install package dependencies)
- `CMD`: the **main** command that will be executed when we run our **Docker image**. There can only be one `CMD` instruction in a `Dockerfile`. It is usually the last instruction!
