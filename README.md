## 🛰️ **Project Name:** Real-Time Sensor Stream with Apache Kafka

### 📖 **Overview**

This project demonstrates basic **streaming data concepts** using **Apache Kafka** and **Python**.
It simulates IoT sensor readings, produces them to a Kafka topic, consumes the data in real time, and performs a simple **10-second windowed count** to show basic event stream processing.

---

### ⚙️ **Architecture**

```
┌──────────────┐     ┌──────────────────┐     ┌──────────────────────┐
│  Sensor Data │ →→→ │ Kafka Producer   │ →→→ │ Kafka Topic: sensor-data │
└──────────────┘     └──────────────────┘     └──────────────────────┘
                                             ↓
                                       ┌─────────────┐
                                       │ Kafka Consumer │
                                       └─────────────┘
                                             ↓
                                       ┌──────────────────────┐
                                       │ Windowed Counter     │
                                       └──────────────────────┘
```

---

### 🧰 **Tech Stack**

* **Python 3**
* **Apache Kafka**
* **Zookeeper**
* **Kafka-Python** library

---

### 🚀 **Setup Instructions**

#### 1️⃣ Install Kafka (on WSL / Linux)

```bash
sudo apt update
sudo apt install openjdk-11-jre-headless -y
wget https://downloads.apache.org/kafka/3.7.0/kafka_2.13-3.7.0.tgz
tar -xvzf kafka_2.13-3.7.0.tgz
cd kafka_2.13-3.7.0
```

#### 2️⃣ Start Zookeeper and Kafka

```bash
# Terminal 1
bin/zookeeper-server-start.sh config/zookeeper.properties
```

```bash
# Terminal 2
bin/kafka-server-start.sh config/server.properties
```

#### 3️⃣ Create the topic

```bash
bin/kafka-topics.sh --create --topic sensor-data --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```

#### 4️⃣ Install Python requirements

```bash
python3 -m venv venv
source venv/bin/activate
pip install kafka-python
```

---

### 📡 **Run the System**

#### 🟢 Producer

```bash
python3 producer.py
```

#### 🟣 Consumer

```bash
python3 consumer.py
```

#### 🔵 Windowed Counter

```bash
python3 windowed_counter.py
```

---

### 🔍 **Example Output**

**Producer**

```
Produced: {'sensor_id': 1, 'temperature': 25.73, 'humidity': 53.1}
Produced: {'sensor_id': 1, 'temperature': 26.18, 'humidity': 49.2}
```

**Consumer**

```
Consumed: {'sensor_id': 1, 'temperature': 25.73, 'humidity': 53.1}
Consumed: {'sensor_id': 1, 'temperature': 26.18, 'humidity': 49.2}
```

**Windowed Counter**

```
Messages in last 10s: 5
Messages in last 10s: 5
Messages in last 10s: 5
```

---

### 📈 **Concepts Demonstrated**

* Real-time data ingestion
* Kafka topics, producers, and consumers
* Simple streaming analytics
* Windowed counting and message batching

---

### 🧠 **Next Steps (Optional Enhancements)**

* Add **sliding windows** (1-second step)
* Store results in **PostgreSQL** or **InfluxDB**
* Create a **dashboard** in Streamlit or Grafana
* Add **error handling and retries** for producers


