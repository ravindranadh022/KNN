# KNN
# K-Nearest Neighbors (KNN) Algorithm

## 1. Introduction

K-Nearest Neighbors (KNN) is a supervised machine learning algorithm used for both classification and regression tasks. It is a simple, non-parametric, instance-based learning algorithm that predicts the output of a new data point by identifying the K closest data points in the training dataset.

KNN follows the principle that similar data points are likely to belong to the same category or have similar output values.

Unlike many other machine learning algorithms, KNN does not explicitly learn a mathematical model during training. Instead, it stores the training dataset and uses it during prediction.

## 2. Working Principle

The KNN algorithm works through the following steps:

1. **Load the Dataset:** Load the training dataset containing input features and target labels.
2. **Choose K:** Select the number of nearest neighbors to consider.
3. **Calculate Distance:** Calculate the distance between the new data point and existing training data points.
4. **Find Nearest Neighbors:** Identify the K data points with the smallest distances.
5. **Perform Voting:** For classification, determine the most frequently occurring class among the nearest neighbors.
6. **Predict Output:** Assign the majority class to the new data point.

## 3. Distance Metrics

KNN uses distance metrics to measure the similarity between data points.

### A. Euclidean Distance

Euclidean distance calculates the straight-line distance between two points.

Formula:

d(x,y) = √Σ(xᵢ - yᵢ)²

### B. Manhattan Distance

Manhattan distance calculates the sum of the absolute differences between corresponding feature values.

Formula:

d(x,y) = Σ|xᵢ - yᵢ|

### C. Minkowski Distance

Minkowski distance is a generalized distance metric that includes both Euclidean and Manhattan distances.

Formula:

d(x,y) = (Σ|xᵢ - yᵢ|ᵖ)^(1/p)

## 4. Types of KNN

### A. KNN Classification

KNN classification is used when the target variable contains categorical values.

Examples:
- Spam or Not Spam.
- Benign or Malicious Network Traffic.
- Fraudulent or Non-Fraudulent Transactions.
- Disease or No Disease.

The algorithm uses majority voting to determine the predicted class.

### B. KNN Regression

KNN regression is used when the target variable contains continuous numerical values.

Examples:
- House Price Prediction.
- Salary Prediction.
- Temperature Prediction.

The algorithm generally calculates the average output of the K nearest neighbors to predict the numerical value.

## 5. Choosing the Value of K

The value of K plays an important role in the performance of the KNN algorithm.

- **Small K:** May lead to overfitting because predictions are highly influenced by individual data points and noise.
- **Large K:** May lead to underfitting because too many neighbors are considered, potentially ignoring local patterns.

The optimal value of K can be selected using cross-validation.

An odd value of K is often preferred in binary classification to reduce the possibility of tied votes.

## 6. Feature Scaling

Feature scaling is an important preprocessing step in KNN because the algorithm relies on distance calculations.

If features have different scales, features with larger numerical values may dominate the distance calculation.

Common scaling techniques include:

### Standardization

Transforms features to have approximately zero mean and unit variance.

### Normalization

Scales feature values into a specified range, commonly between 0 and 1.

StandardScaler and MinMaxScaler from Scikit-learn can be used for this purpose.

## 7. Advantages of KNN

- Simple and easy to understand.
- Easy to implement.
- Supports classification and regression.
- Does not require an explicit training phase.
- Can handle multiclass classification.
- Makes no strong assumptions about the underlying data distribution.

## 8. Disadvantages of KNN

- Prediction can be computationally expensive for large datasets.
- Requires storing the complete training dataset.
- Sensitive to irrelevant features and noisy data.
- Performance depends heavily on the selection of K.
- Sensitive to feature scaling.
- Performance can decrease in high-dimensional datasets due to the curse of dimensionality.

## 9. Applications of KNN

KNN is widely used in different domains:

- **Healthcare:** Disease classification and medical diagnosis.
- **Cybersecurity:** Network intrusion detection and malicious traffic classification.
- **Finance:** Fraud detection and credit risk assessment.
- **Recommendation Systems:** Finding similar users or products.
- **Image Recognition:** Identifying objects based on feature similarity.
- **Pattern Recognition:** Recognizing patterns in datasets.

## 10. Implementation Using Python

### Required Libraries

```bash
pip install numpy pandas scikit-learn matplotlib seaborn
```

### Python Example

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import accuracy_score, classification_report

# Load dataset
data = pd.read_csv("dataset.csv")

# Separate features and target
X = data.drop("target", axis=1)
y = data["target"]

# Split dataset
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Feature scaling
scaler = StandardScaler()

X_train = scaler.fit_transform(X_train)
X_test = scaler.transform(X_test)

# Initialize KNN model
knn = KNeighborsClassifier(n_neighbors=5)

# Train model
knn.fit(X_train, y_train)

# Make predictions
y_pred = knn.predict(X_test)

# Evaluate model
print("Accuracy:", accuracy_score(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

**Note:** Replace `dataset.csv` with your dataset filename and `target` with the actual target column name.

## 11. Performance Evaluation Metrics

The performance of the KNN classification model can be evaluated using:

- **Accuracy:** Measures the percentage of correctly classified predictions.
- **Precision:** Measures how many predicted positive instances are actually positive.
- **Recall:** Measures how many actual positive instances are correctly identified.
- **F1-Score:** Calculates the harmonic mean of precision and recall.
- **Confusion Matrix:** Provides a detailed comparison of actual and predicted classes.

## 12. Conclusion

K-Nearest Neighbors is a simple yet effective supervised machine learning algorithm that classifies or predicts new data points based on their similarity to existing observations.

Its simplicity, flexibility, and ability to solve both classification and regression problems make it useful in various applications, including healthcare, finance, pattern recognition, and cybersecurity.

However, proper feature scaling, selection of an appropriate K value, and choosing a suitable distance metric are important for achieving better performance.

















services:

  web:
    image: nginx:latest
    ports:
      - "8080:80"

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: demo
      POSTGRES_PASSWORD: demo
      POSTGRES_DB: demo_db



services:

  web:
    image: nginx:latest
    ports:
      - "8081:80"
    depends_on:
      - redis

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: demo
      POSTGRES_PASSWORD: demo
      POSTGRES_DB: demo_db

  redis:
    image: redis:alpine




Networking and volume

services:
  web:
    image: nginx:latest
    ports:
      - "8081:80"
    depends_on:
      - db
    networks:
      - app-net

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: demo
      POSTGRES_PASSWORD: demo
      POSTGRES_DB: demo_db
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - app-net

  redis:
    image: redis:alpine

networks:
  app-net:

volumes:
  db-data:


commands
# 1. Start all containers
docker compose up -d

# 2. Check running containers
docker compose ps

# 3. List Docker networks
docker network ls

# 4. List Docker volumes
docker volume ls

# 5. Enter PostgreSQL container
docker compose exec db psql -U demo -d demo_db

# 6. Create students table
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50)
);

# 7. Insert records
INSERT INTO students (name) VALUES ('Ravi');
INSERT INTO students (name) VALUES ('Vamsi');

# 8. Display records
SELECT * FROM students;

# 9. Exit PostgreSQL
\q

# 10. Stop and remove containers
docker compose down

# 11. Start containers again
docker compose up -d

# 12. Enter PostgreSQL again
docker compose exec db psql -U demo -d demo_db

# 13. Verify persistent storage
SELECT * FROM students;

# 14. Exit PostgreSQL
\q

# 15. Check containers
docker ps









Own Image    app.py
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from Flask + Docker hello!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)



Dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY app.py /app/

RUN pip install flask                     //docker compose up --build

CMD ["python", "app.py"]







docker compose up --build -d

docker ps

docker compose ps

docker build -t flask-docker-app .

docker images

docker compose down

docker run -d -p 5000:5000 --name flask-container flask-docker-app

docker ps

docker stop flask-container

docker rm flask-container

docker login

docker tag flask-docker-app YOUR_USERNAME/flask-docker-app:latest

docker images

docker push YOUR_USERNAME/flask-docker-app:latest

docker login

docker pull YOUR_USERNAME/flask-docker-app:latest

docker run -d -p 5000:5000 --name flask-container YOUR_USERNAME/flask-docker-app:latest

docker ps
