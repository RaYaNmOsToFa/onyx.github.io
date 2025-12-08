# P4 - MapReduce

*A lightweight distributed MapReduce framework in Python*

<img width="700" height="200" alt="image" src="https://github.com/user-attachments/assets/cd61e349-bf36-44de-ae27-c0ba0c85543a" />

---

## 💡 TLDR: What is MapReduce? {#tldr}

MapReduce is a simple, powerful concept for processing **huge amounts of data** by breaking the task into many small, manageable pieces and solving them simultaneously across many computers.

Think of it like sorting and summarizing a massive library's worth of books (like a **Word Count**):

1.  **The "Map" Step (The Break-up):** Instead of one person reading every book, you hire hundreds of assistants (the **Workers**). You give each assistant a small stack of books and tell them to find every instance of a specific word and note the word itself along with a count of '1'. This is the **parallel processing** step.
2.  **The "Shuffle" Step (The Organization):** You collect all the notes from the hundreds of assistants. Then, you organize these notes by the specific word you were tracking. All the notes for "aardvark" go into one pile, all the notes for "zebra" go into another, and so on.
3.  **The "Reduce" Step (The Summary):** Now, you give each word-specific pile to a new set of assistants. Their job is to summarize that pile—for example, by counting up all the '1's associated with "aardvark" to get its total count. This summary is the final, consolidated result.

**The result:** A job that would take one person a year is finished by a team in hours, and if one assistant gets sick, the others just pick up their stack (that's **fault tolerance**)! This project, **P4 - MapReduce**, is a simplified version of this system written in Python.

---

## 📖 Table of Contents
- [About the Project](#about-the-project)
- [💡 TLDR: What is MapReduce?](#tldr)
- [Architecture](#architecture)
- [Features](#features)
- [Quickstart / Installation](#quickstart--installation)
- [Usage Examples](#usage-examples)
- [Architecture-Diagram](#architecture-Diagram)
- [FAQ](#faq)
- [Contributing](#contributing)
- [License](#license)

---

## About the Project {#about-the-project}
**P4 - MapReduce** is a simple, educational implementation of the MapReduce paradigm written in Python.
It simulates a distributed computing environment, where:

- A **Manager node** distributes jobs and coordinates execution.
- Multiple **Worker nodes** process chunks of data in parallel.

This project is designed for students, researchers, or developers who want to understand distributed computation concepts like task scheduling, parallel execution, and fault tolerance at a small scale.

---

## Architecture {#architecture}

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

## Features {#features}
- Distributed job execution using socket-based communication
- Parallel processing of tasks across multiple worker nodes
- Custom user-defined `map()` and `reduce()` functions
- Automatic retry on worker failure
- Fault tolerance through heartbeat messages.

---

## Quickstart / Installation {#quickstart--installation}

### 1. Clone and install
```bash
git clone [https://github.com/RaYaNmOsToFa/p4-mapreduce/](https://github.com/RaYaNmOsToFa/p4-mapreduce/)
cd p4-mapreduce
python -m venv venv
source venv/bin/activate    # (or venv\Scripts\activate on Windows)
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

### 4. End Processes
```bash
python3 submit.py --shutdown
```

## Usage Examples {#usage-examples}
A classic example for MapReduce is Word Count. The goal is to count the frequency of every word in a large set of text files.

Sample Input
Imagine the input files contain the following text:

input/file_a.txt -> the cat sat on the mat
input/file_b.txt ->	a cat is a cat

**Example Map/Reduce Functions**
<table>
  <tr>
    <th>Phase</th>
    <th>Function</th>
    <th>Description</th>
    <th>Output Format</th>
  </tr>
  <tr>
    <td>Map</td>
    <td>mapper(line)</td>
    <td>For each word in the input line, it emits the word and a count of 1.</td>
    <td><word>, 1</td>
  </tr>
  <tr>
    <td>Reduce</td>
    <td>reducer(key, values)</td>
    <td>Takes a unique word (key) and a list of all its intermediate counts (values - all 1s). Sums the counts.</td>
    <td><word>, total_count</td>
  </tr>
</table>

### 1. Map Output (Intermediate):
```bash
the, 1
cat, 1
sat, 1
on, 1
the, 1
mat, 1
a, 1
cat, 1
is, 1
a, 1
cat, 1
```
### 2. Shuffle & Group:
```bash
a: [1, 1]
cat: [1, 1, 1]
is: [1]
mat: [1]
on: [1]
sat: [1]
the: [1, 1]
```
### 3. Reduce Output (Final):
```bash
a, 2
cat, 3
is, 1
mat, 1
on, 1
sat, 1
the, 2
```

## Architecture Diagram {#architecture-Diagram}
<img width="1551" height="710" alt="image" src="https://github.com/user-attachments/assets/065bc230-6c68-4b00-a3e0-2cdac793dbf3" />

## FAQ {#faq}
Q: Does this require multiple physical machines? A: No — you can run multiple worker processes on a single machine for simulation (you must have available ports however).

Q: Is this production-ready? A: No — this is an educational project meant for learning distributed systems principles.

Q: Can I add more workers dynamically? A: Yes — new workers can connect to the manager while it’s running (and manager can tell when workers die as well).

## Contributing {#contributing}
Things are kind of done around here. Please don't cheat...

## License {#license}
There is no license... Please follow the EECS honor code...






