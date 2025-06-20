NAME OF PROJECT: Project 1: Implement File Server
=================================================

MEMBERS: Noah Storms
===================================

STATEMENT: 
===========
We have neither given nor received unauthorized assistance on this work.

HOW TO ACCESS:
==============
Open two terminals, one for the server and one for the client.

Compile the server and client code using gcc:

Terminal 1 (Server):

	gcc -o server udp_server.c

Terminal 2 (Client):

	gcc -o client udp_client.c

Run the server and client in different terminals:

Terminal 1 (Server side):

	./server

Terminal 2 (Client side):

	./client <server_hostname>

Client Menu:
Once the client starts, you'll be prompted to enter a command in the format:

	[protocol_type] [file_name] [drop_percentage]

Example:
- Stop-and-Wait Protocol (with 10% packet drop):
	1 testfile.txt 10

- Go-Back-N Protocol (with 20% packet drop):
	2 testfile.txt 20

Protocol Options:
- Stop-and-Wait (SW): Enter 1 for Stop-and-Wait protocol.
- Go-Back-N (GBN): Enter 2 for Go-Back-N protocol.

Exit Command:
- To exit the client program and stop the server, type:
	
	- exit

PROJECT DESCRIPTION:
====================
This project implements a client-server system using UDP to transmit files with simulated packet loss. It supports two ARQ (Automatic Repeat request) protocols: 

	1. Stop-and-Wait (SW)
	2. Go-Back-N (GBN) 

allowing the server to send files reliably over an unreliable network.

Key Features:
- UDP Communication: The project uses UDP for communication between the client and server.
- Packet Loss Simulation: The server simulates packet loss based on a percentage provided by the client.
- ARQ Protocols:
	- Stop-and-Wait: The client acknowledges each packet before the server sends the next one.
	- Go-Back-N: The server can send multiple packets before waiting for acknowledgments, but it retransmits unacknowledged packets if
	an error occurs.

Files:
======
udp_server.c:
==============
The server-side program that listens for file requests from the client. It simulates packet loss based on the client's input and uses either the Stop-and-Wait or Go-Back-N ARQ protocol to ensure reliable delivery.

Key functionalities:
- Listens for client requests.
- Simulates packet drops.
- Implements Stop-and-Wait and Go-Back-N protocols.

udp_client.c:
==============
The client-side program that requests a file from the server using either the Stop-and-Wait or Go-Back-N ARQ protocol.

Key functionalities:
- Sends file requests.
- Receives file data in chunks and acknowledges packets.
- Handles retransmissions in case of packet loss.

CHALLENGES OVERCAME:
========================
- Initial Connection Setup: We initially struggled to establish a reliable connection between the client and server. We used the  resources provided to us, textbook and example code (udpclient.c and udpserver.c), which helped us resolve connectivity issues and more.

- Protocol Implementation: Implementing the Stop and Wait and Go Back N protocols presented challenges. We created print messages for debugging, ensuring communication between the client and server. This approach helped with identifying and resolving protocol-related issues.

- File Transfer Integrity: One persistent issue was ensuring the integrity of file transfers. Initially, the client received files that didn't reflect requested changes. We addressed this by modifying our server to create a new file for each requested transfer, ensuring accurate data delivery.

- Frame Dropping/Mixup: Our server had irregularity experiences frame drops during file transmissions. While the overall percentage of dropped frames remains consistent, some files were incompletely transmitted due to text exceeding frame size limits. This happened in both SW and GBN parts.

- Exiting: After running GBN, the server automatically terminates without exit prompt. This problem has not been solved which means the server needs to be re-launched each time the client wants to run.

RESOURCES & DISCUSSIONS:
========================

Textbook:
Referenced Chapter 5 (ARQ algorithms) and Chapter 6 (Berkeley Sockets and example socket programming) for guidance on socket programming and ARQ protocols.

Canvas:
Example code of udpclient.c and udpserver.c
