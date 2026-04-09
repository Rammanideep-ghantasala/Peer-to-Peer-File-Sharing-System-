# 📂 Peer-to-Peer File Sharing System

## 🚀 Description

This project implements a decentralized Peer-to-Peer (P2P) file sharing system using C++ and socket programming. Files are divided into chunks and distributed across multiple peers. A tracker is used to coordinate communication, manage metadata, and maintain information about peers sharing files.

The system supports file upload, download, chunk-based transfer, SHA-1 hashing for data integrity, and group-based file sharing.

---

## ✨ Features

* 🔗 Peer-to-peer file sharing without a central server
* 📦 File chunking (512 KB per chunk)
* 🔐 SHA-1 hashing for file and chunk integrity
* 👥 Group-based file sharing system
* 🔄 Multi-peer file downloading
* 🧵 Multithreading with mutex locks for synchronization
* 🌐 TCP/IP socket-based communication

---

## 🛠️ Tech Stack

* C++
* Socket Programming (TCP/IP)
* Multithreading (POSIX Threads)
* OpenSSL (SHA-1 hashing)

---

## 📁 Project Structure

```
.
├── tracker.cpp
├── client.cpp
├── tracker_info.txt
├── README.md
```

---

## ⚙️ Tracker (tracker.cpp)

### 📌 Overview

The tracker is responsible for managing users, groups, and file metadata. It maintains information about available files and the peers that hold them.

### 🔹 Libraries and Headers

* Standard C++ libraries
* Networking: `sys/socket.h`, `netinet/in.h`, `arpa/inet.h`
* OpenSSL: `<openssl/sha.h>`

### 🔹 Global Data Structures

* `userdetails` → Stores user credentials
* `groups` → Maps group ID to admin
* `pendingrequests` → Tracks join requests
* `groupmembers` → Stores group members
* `ipandport` → Stores active user IPs and ports
* `groupfiles` → Stores shared files in groups
* `groupfileinfo` → Stores file metadata (paths, hashes, peers)

### 🔹 Helper Structures

* `ipports` → Stores IP and port
* `filepeerinfo` → Stores file SHA, chunk hashes, and peers

### 🔹 Multithreading

* Uses mutex locks to ensure thread-safe access to shared resources

### 🔹 Functionalities

#### 👤 User Operations

* `createuser()` → Create a new user
* `loginuser()` → Authenticate user and store connection info

#### 👥 Group Operations

* `creategroup()` → Create a new group
* `joingroup()` → Request to join a group
* `leavegroup()` → Leave group / handle admin changes
* `listrequests()` → View pending requests
* `acceptrequest()` → Approve join requests
* `listallgroups()` → Display all groups

#### 📂 File Operations

* `uploadfile()` → Upload file and store metadata
* `handleDownloadRequest()` → Provide file info for download

#### 🔧 Utility Functions

* `split()` → Command parsing
* `ipport()` → Store client IP and port
* `trackerinformation()` → Read tracker configuration

---

## 💻 Client (client.cpp)

### 📌 Overview

The client acts as a peer in the network. It can upload, download, and share file chunks with other peers.

### 🔹 Key Features

#### 📦 File Chunking & Hashing

* Files are split into 512 KB chunks
* SHA-1 hash computed for each chunk
* Overall file hash ensures integrity

#### 🔗 Peer-to-Peer Transfer

* Peers request specific chunks from other peers
* Each peer runs a listener to serve chunk requests

#### 🌐 Tracker Communication

* Connects to tracker for metadata and peer details
* Retrieves chunk and peer information for downloads

---

### 🔹 Core Structures

```cpp
struct Chunk {
    string sha1hash;
    vector<char> data;
};

struct FileInfo {
    string filename;
    string overallsha;
    vector<Chunk> chunks;
};
```

---

### 🔹 Important Functions

* `SHA1calculation()` → Computes SHA-1 hash
* `processFile()` → Splits file and computes hashes
* `connecttotracker()` → Establishes tracker connection
* `clientlistener()` → Handles incoming peer requests
* `downloadFile()` → Downloads file from peers
* `trackerfileopen()` → Reads tracker configuration

---

## ▶️ How to Run

### 🔹 Step 1: Compile

```bash
g++ -o tracker tracker.cpp -lpthread -lssl -lcrypto
g++ -o client client.cpp -lssl -lcrypto
```

### 🔹 Step 2: Run Tracker

```bash
./tracker tracker_info.txt tracker_id
```

### 🔹 Step 3: Run Client

```bash
./client ip:port tracker_info.txt
```

---

## 📸 Sample Commands

```
create_user user1 pass123  
login user1 pass123  
create_group group1  
join_group group1  
upload_file file.txt group1  
download_file group1 file.txt destination_path  
```

---

## 🔐 Key Concepts Used

* Peer-to-Peer Networking
* Distributed Systems
* Socket Programming
* File Chunking
* Cryptographic Hashing (SHA-1)
* Multithreading & Synchronization

---

## 📌 Conclusion

This project demonstrates a scalable and efficient decentralized file sharing system. It highlights concepts of distributed systems, networking, and data integrity through chunk-based file transfer and peer coordination.

---
