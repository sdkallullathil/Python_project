<h1>Developing a Client-Server Text-Based Chat Application: Python Project</h1>


<h2>Description</h2>

<p>The project initiates with the development of a fundamental client-server infrastructure designed for a text-based chat application. Beyond facilitating basic communication, the application introduces an engaging feature by seamlessly integrating jokes retrieved from an external API upon user request. The server script skillfully establishes a socket using the socket module, adeptly handling incoming connections, and ensuring secure client interactions by prompting users for username and password authentication.<br/>

To fortify the confidentiality and integrity of the transmitted data, SSL/TLS encryption is strategically implemented using the ssl module. The integration of OpenSSL further enhances the security posture, as self-signed certificates are generated to establish a robust SSL/TLS setup.<br/>

In addition to the technical prowess demonstrated in establishing a secure communication channel, the project prioritizes security by meticulously managing errors. This deliberate focus on error handling contributes to the application's overall robustness, reducing vulnerabilities and ensuring a resilient and secure user experience. The combination of fundamental client-server functionality, the introduction of an API-driven joke feature, and the incorporation of SSL/TLS encryption and error management collectively underscores the project's commitment to achieving a well-rounded, secure, and user-friendly application.


<h2>Utilities Used</h2>

<h3>Python Libraries: </h3>

- <b>ssl</b>
- <b>urllib</b>
- <b>requests</b>
- <b>request.exceptions</b>
- <b>response</b>
- <b>json</b>
- <b>sockets</b>
- <b>bcrypt</b>
- <b>hashlib</b>
- <b>gtoken</b>
- <b>logging</b>
- <b>smtplib</b>

<br/>
<h2>Project Components</h2>
<br/>
- <b>server.py</b>: Handles server-side operations, authentication, and integration of the joke feature.<br/><br/>
- <b>client.py</b>: Manages client-side operations, authentication, and integration of the joke feature. <br/><br/>
- <b>joke_module.py</b>: Contains the get_joke() function responsible for making API calls and displaying jokes.
<br/><br/>




<h2>Client-Server Interaction</h2>


In the server-side Python script, a <b>socket</b> is instantiated through the use of the socket module, binding it to a specified IP address and port number. The server actively listens for incoming connections, notifying the establishment of a connection by printing a corresponding message. Upon successful connection, the server prompts the client to provide a username and password. The entered password is then compared to a pre-defined username and its hashed counterpart. If the password hashes match, the server grants access to the client, initiating a chat loop.

Similarly, within the client's Python script, a socket is created, establishing a connection with the server's IP address and port. The client is then prompted to input a username and password, which are subsequently transmitted to the server for authentication. Following a successful authentication process, the client seamlessly enters a chat loop, enabling the exchange of messages with the server. This interactive conversation persists until either participant types 'end,' indicating the desire to conclude the connection. The specific example provided, with the host set as '127.0.0.1' and port number 9001, illustrates a practical implementation of these communication channels in a local environment.


<br/>
<img src="https://github.com/sdkallullathil/Python_project/blob/276c15eca3a81b203e2d73bb73c242423f868e78/server-1.png" height="90%" width="90%" alt="Disk Sanitization Steps"/>
<br />

<br/>
<img src="https://github.com/sdkallullathil/Python_project/blob/276c15eca3a81b203e2d73bb73c242423f868e78/server-2.png" height="90%" width="90%" alt="Disk Sanitization Steps"/>
<br />

<h2>Password Security</h2>


<h3> Hashing Passwords:</h3>
The project demonstrates a robust approach to password security through the implementation of scripts showcasing the secure hashing of passwords. Utilizing industry-standard algorithms, specifically the <b>sha256</b> hash function from the <b>hashlib</b> library, the project prioritizes enhancing user account security. To further safeguard sensitive information, the username and corresponding hashed passwords are deliberately stored on the server side, maintaining an additional layer of protection. Importantly, these credentials are strategically managed in a separate script, namely <b>credentials.json</b>, ensuring that sensitive data remains discreet and does not appear directly in the main code (<b>server.py</b>).

<h3> Password Hash Checks:</h3> 
Upon initiating communication, the client is prompted to provide credentials, comprising a username and password with <b>client.py</b> script. The server side meticulously converts this input into hashed values, employing the same hashing algorithm used during the initial password creation. Subsequently, these hashed values are verified against the stored password hashes for authentication purposes. Access to the chat application is granted only if the hashed passwords match, emphasizing the importance of secure authentication.<br/><br/>

<br/>
<img src="https://github.com/sdkallullathil/Python_project/blob/276c15eca3a81b203e2d73bb73c242423f868e78/client.png" height="90%" width="90%" alt="Disk Sanitization Steps"/>
<br />

Incorporating an added layer of security, the system limits the client to three password attempts. In the event of an incorrect password entry, the system intelligently communicates the remaining number of trials. If the client surpasses three unsuccessful attempts, access is denied, enhancing security measures by preventing further password trials. This multi-faceted approach underscores the commitment to robust password security and user authentication within the project.







<h2>SSL/TLS Encryption Implementation</h2>

To bolster the project's security measures, a pivotal improvement centers around the incorporation of `SSL/TLS` encryption through the utilization of the ssl module. This encryption mechanism ensures that all data exchanged between the server and client is meticulously secured, thwarting potential eavesdropping attempts and unauthorized access. By establishing an encrypted communication channel, this enhancement plays a crucial role in fortifying the protection of sensitive information, creating a more robust and secure environment for the text-based chat application.

For the generation of server and client certificates, OpenSSL was employed to create self-signed certificates specifically tailored for the SSL/TLS setup. While self-signed certificates are suitable for testing and development purposes, it is imperative to note that, in a real-world scenario, certificates from a trusted Certificate Authority (CA) would be acquired. This step is essential for elevating the security posture of the system, ensuring the authenticity of the certificates, and maintaining the highest standards of security in a production environment.



<h2>Generation of Server and Client certificates with OpenSSL</h2>

To generate server and client certificates, `OpenSSL`, a versatile open-source toolkit, is employed. OpenSSL facilitates the creation of self-signed certificates, which are suitable for testing and development purposes. The process begins by generating a Certificate Authority (CA) key and certificate. The CA key is created using the RSA algorithm, and a corresponding Certificate Signing Request (CSR) is generated. Subsequently, the CA certificate is self-signed, serving as the root of trust for the ensuing certificates.

For the server, a private key is generated, and a CSR is crafted. The server certificate is then signed by the CA, establishing a secure identity for the server. Similarly, on the client side, a private key and CSR are generated, and the resulting client certificate is signed by the CA. These certificates, along with their respective private keys, form the cryptographic foundation for secure communication.

While these self-signed certificates are suitable for testing, in a real-world scenario, it is crucial to obtain certificates from a trusted Certificate Authority (CA) to ensure authenticity and adherence to the highest security standards. This multi-layered approach, combining SSL/TLS encryption and the utilization of OpenSSL for certificate generation, underscores the project's commitment to robust security practices.

<h4>Resulting Files:</h4>

- <b>ca.crt:</b> CA certificate (public key)
- <b>ca.key:</b> CA private key
- <b>server_cert.pem:</b> Server certificate (public key)
- <b>server_key.pem:</b> Server private key
- <b>client_cert.pem:</b> Client certificate (public key)
- <b>client_key.pem:</b> Client private key




<h2>Joke Integration</h2>

The project incorporates an innovative feature through the introduction of the `get_joke()` function, strategically placed within a dedicated module named `joke_module.py`. This modular design promotes code organization and clarity, encapsulating the functionality related to joke retrieval.

Implemented using the `requests` module, the `get_joke()` function seamlessly executes an <b>API</b> call to fetch a random joke from the external API hosted at <b>official-joke-api.appspot.com</b>. This external API serves as a dynamic source of humor, adding an engaging and entertaining element to the chat application.

Both the server and client scripts undergo thoughtful modifications to integrate the logic for requesting jokes seamlessly into the chat loop. Users can trigger the joke retrieval process by entering the command "get_joke" during their interaction.

Upon receiving the request, the `get_joke()` function is promptly invoked. The retrieved joke, presented in either a single or two-part format, is then elegantly displayed within the chat interface. This enhancement not only contributes to a more enjoyable user experience but also showcases the project's adaptability in incorporating diverse functionalities, extending beyond conventional text-based communication.

<br/>
<img src="https://github.com/sdkallullathil/Python_project/blob/276c15eca3a81b203e2d73bb73c242423f868e78/joke.png" height="90%" width="90%" alt="Disk Sanitization Steps"/>
<br />

<h2>Robust Error Handling</h2>


Another pivotal aspect of the security enhancements revolves around the integration of robust error handling mechanisms, meticulously implemented through the use of try-except blocks. This approach aims to ensure a more reliable and secure operation of the application by gracefully handling exceptions that may arise during execution. Error handling becomes particularly crucial in the context of security, as it prevents potential vulnerabilities and ensures that unexpected situations are managed in a controlled manner. By proactively addressing errors, the project not only enhances its overall stability but also mitigates potential security risks, contributing to a more resilient and dependable system. This commitment to error handling aligns with best practices in secure software development and reinforces the project's dedication to providing a secure user experience.

<h2>Conclusions</h2>

In conclusion, the developed text-based chat application stands as a testament to the successful integration of security, user-friendly features, and modular coding practices. The implementation prioritizes data protection through the incorporation of SSL/TLS encryption, addressing a critical vulnerability. Robust password security is ensured by securely hashing passwords, and the introduction of the get_joke() function enhances user engagement, offering a playful and interactive element to conversations.

The project's organized and modular code structure, coupled with robust error handling, contributes to code clarity and stability. The platform is adaptable, demonstrated by its seamless integration of new features. While the application utilizes self-signed certificates for testing, it underscores the importance of obtaining certificates from trusted Certificate Authorities (CAs) for production scenarios. Overall, the project sets the stage for a secure, extensible, and user-centric text-based communication platform.

