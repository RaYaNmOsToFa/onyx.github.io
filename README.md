# P4 - MapReduce

<!-- TODO: Add your project logo or banner here -->
<!-- ![PyMapReduce Logo](docs/logo.png) -->

*A lightweight distributed MapReduce framework in Python*

<img width="700" height="200" alt="image" src="https://github.com/user-attachments/assets/cd61e349-bf36-44de-ae27-c0ba0c85543a" />



---

## 📖 Table of Contents
- [About the Project](#-about-the-project)
- [Architecture](#-architecture)
- [Features](#-features)
- [Quickstart / Installation](#-quickstart--installation)
- [Usage Examples](#-usage-examples)
- [FAQ](#-faq)
- [Contributing](#-contributing)

---

## About the Project
**P4 - MapReduce** is a simple, educational implementation of the MapReduce paradigm written in Python.  
It simulates a distributed computing environment, where:

- A **Manager node** distributes jobs and coordinates execution.
- Multiple **Worker nodes** process chunks of data in parallel.

This project is designed for students, researchers, or developers who want to understand distributed computation concepts like task scheduling, parallel execution, and fault tolerance at a small scale.

---

## Architecture

<!-- TODO: Insert architecture diagram image here -->
<!-- ![Architecture Diagram](docs/architecture.png) -->

**Components:**
- **Manager**: Receives a job, splits data into chunks, assigns tasks to workers, and collects results.
- **Workers**: Receive tasks from the manager, run user-defined `map` and `reduce` functions, and return intermediate/final outputs.
- **Utila**: Utility directory that contains networking functions to send/receive messages using UDP or TCP networking protocos and a class for a thread safe dict.

**Workflow:**
1. Manager splits input data.
2. Workers run `map()` on data chunks and emit key-value pairs.
3. Manager shuffles & groups pairs by key (creating temporary directories)
4. Workers run `reduce()` on grouped data.
5. Manager collects final output.

---

## Features
- Distributed job execution using socket-based communication
- Parallel processing of tasks across multiple worker nodes
- Custom user-defined `map()` and `reduce()` functions
- Automatic retry on worker failure
- Fault tolerance through heartbeat messages. 

---

## Quickstart / Installation

### 1. Clone and install
```bash
git clone https://github.com/RaYaNmOsToFa/p4-mapreduce/
cd p4-mapreduce
python -m venv venv
source venv/bin/activate    # (or venv\Scripts\activate on Windows)
pip install -r requirements.txt
```

### 2. Start the Processes
```bash
chmod +x /bin/mapreduce
./bin/mapreduce start
```

### 3. Submit a Job
```bash
python3 submit.py -h <host> -p <port> -i <input_directory> -o <output_directory> -m <mapper_executable> -r <reducer_executable> --nreducers <num_mappers> --nreducers <num_reducers>
```

### 4. End Porcesses
```bash
python3 submit.py --shutdown
```

## Architecture Diagram 
<img width="1551" height="710" alt="image" src="https://github.com/user-attachments/assets/065bc230-6c68-4b00-a3e0-2cdac793dbf3" />

## FAQ
Q: Does this require multiple physical machines?
A: No — you can run multiple worker processes on a single machine for simulation (you must have available ports however).

Q: Is this production-ready?
A: No — this is an educational project meant for learning distributed systems principles.

Q: Can I add more workers dynamically?
A: Yes — new workers can connect to the manager while it’s running (and manager can tell when workers die as well).

## Contributing
Things are kind of done around here. Please don't cheat...

## License
There is no license... Please follow the EECS honor code...
