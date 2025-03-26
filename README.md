 Full Packet-Level Analysis of a Web Request
This project was a deep dive into tracking a single web request from start to finish, analyzing each stage at the packet level using Wireshark. By working through DNS resolution, the TCP handshake, and the TLS handshake, you’ve gained an advanced, real-world understanding of encrypted communications at the network level.

Below is a comprehensive summary of everything we covered, structured in a way that reinforces key takeaways and makes future projects even more efficient.

📌 High-Level Overview of What We Accomplished
1️⃣ Resolved the domain name (DNS resolution)
2️⃣ Established a connection (TCP handshake)
3️⃣ Negotiated secure encryption (TLS handshake)
4️⃣ Validated when encryption begins
5️⃣ Observed encrypted data transmission

We followed each step with precision, ensuring that every data exchange in this process was fully understood.

1️⃣ DNS Resolution: Finding the IP Address
Goal: Convert weightlifting.com into an IP address.

🔹 DNS Queries (A & AAAA)

Our system first requested both an IPv4 (A) and an IPv6 (AAAA) record.

The router did not support IPv6, so only an IPv4 address was returned.

This determined that the connection would proceed over IPv4.

🔹 Key takeaway:

The system first asks if the website supports IPv6 but falls back to IPv4 if necessary.

🛠️ Analogy:
Think of this like asking a store if they accept credit cards (IPv6). If they say no, you use cash (IPv4).

2️⃣ TCP Handshake: Establishing a Connection
Goal: Confirm both the client and server are ready to communicate.

🔹 Three-Way Handshake (SYN → SYN-ACK → ACK)

The client initiated a connection using SYN.

The server acknowledged with SYN-ACK.

The client finalized the handshake with ACK.

This established a reliable connection.

🔹 Negotiated TCP Parameters:

Window size scaling: Allowed for large data transfers.

Maximum segment size (MSS): Defined how much data fits in each packet.

Selective acknowledgments (SACK): Allowed efficient retransmission.

🛠️ Analogy:
Think of this like introducing yourself before a conversation:

"Hi, can we talk?" (SYN)

"Yes, we can talk." (SYN-ACK)

"Great, let's start." (ACK)

3️⃣ TLS Handshake: Securing the Connection
Goal: Encrypt communication using TLS.

🔹 Client Hello (Packet 19)

Sent supported encryption methods (cipher suites) to the server.

Used Server Name Indication (SNI) to specify the domain.

Listed supported TLS versions.

🔹 Server Hello (Packet 21)

Selected TLS 1.3 as the encryption protocol.

Picked TLS_AES_128_GCM_SHA256 as the encryption method.

Sent its public key for key exchange (X25519 curve).

🔹 Key Exchange & Encryption Setup

Both sides agreed on a shared session key for symmetric encryption.

After the Change Cipher Spec message, all communication was encrypted.

🔹 Key takeaway:

TLS 1.3 eliminates unnecessary steps from TLS 1.2, making it faster and more secure.

After the handshake, the session is encrypted—we can see the traffic, but not the content.

🛠️ Analogy:

Client Hello: "I speak English, Spanish, and French. What about you?"

Server Hello: "Great! Let’s talk in Spanish (TLS_AES_128_GCM_SHA256)."

Key Exchange: "Let’s use a secret code to talk privately."

Change Cipher Spec: "From now on, everything we say is encrypted."

4️⃣ Transition to Encrypted Data
Goal: Confirm when encryption starts and data transmission begins.

🔹 The Client Finished message (Packet 26)

This confirmed that the client accepted encryption settings.

Everything after this was fully encrypted.

🔹 Application Data Packets (22, 23, etc.)

These contained actual website requests and responses.

Wireshark could see packet structure but not content.

🛠️ Analogy:
This is like switching from normal conversation to a secret language:

Before: Everyone understands you.

After: Only you and your friend can decrypt the conversation.

