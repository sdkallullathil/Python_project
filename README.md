<h1>Python Scripting</h1>


<h2>Description</h2>
<p>This Python project is dedicated to the development of a comprehensive set of scripts, primarily centered around the task of sending emails by extracting content from an API using Python scripts. While the primary objective is email communication, the project delves into the multifaceted utility of Python by meticulously crafting scripts that not only achieve the specified email functionality but also exemplify best practices in a range of areas.<br/>

The scripts showcase expertise in handling errors with precision, making efficient API calls, establishing network communication through sockets, implementing robust password security mechanisms with hashing techniques, enabling secure authentication in web applications, and proficiently managing various file operations. This project serves as a versatile exploration of Python's capabilities, providing a practical guide for developers to leverage these functionalities in their projects effectively.<br/>


<h2>Utilities Used</h2>

<h3>Python Libraries: </h3>

- <b>urllib</b>
- <b>requests</b>
- <b>request.exceptions</b>
- <b>response</b>
- <b>json</b>
- <b>sockets</b>
- <b>bcrypt</b>
- <b>gtoken</b>
- <b>logging</b>
- <b>smtplib</b>



<h2>Overview</h2>

This Python script is crafted to deliver jokes by utilizing API calls, and it operates as a command-line application. Users securely authenticate with their credentials, which are securely stored on the server. The passwords are stored in a hashed form. During the sign-in process, the script compares the entered hash with the stored hash to determine whether to grant the client access to the application.<br/>

Upon successful authentication, the client is presented with a list of topics. Once a topic is selected, a joke is provided to the client. For added convenience, clients have the option to receive the joke via email. They can securely log in to their email accounts within the application and send the chosen joke to another email address. This feature ensures a seamless and secure experience for users interacting with the script.


<h2>Pcap File Analysis</h2>

Obtained purposefully crafted pcap files designed for malware analysis from malware-traffic-analysis.net. Directed the analysis towards an incident associated with the Boleto malware, notorious for its engagement in the theft of bank details in Brazil. Utilized Wireshark for the analysis, revealing multiple Indicators of Compromise (IOCs) that shed light on the evolution of the attack.<br/>

<h4>Indicators of Compromise (IOCs)</h4> 

Upon conducting a meticulous analysis of the Packet Capture (pcap) using Wireshark's statistics for high-level examination and conversation filters to discern the nature of interactions, port numbers, IPs, and MAC addresses involved, the following key findings have been identified:<br/>
<br/>
<b>Infected computer and user details:</b>
- Date and Time: The traffic initiated on Saturday, 2016-12-17, at approximately 02:30 UTC.
- MAC Address : 00:1c:23:9b:70:5e (Dell)
- IP Address : 172.16.2.96
- Host Name : Froggy-PC
- Account Name: Matthew.Frogman
- Public IP : 201.16.144.112
- Country : Brazil<br/>

Additionally, the analysis reveals that the attack was initiated with the following packet:<br/>
<br/>
Packet Information: <b>65.181.125.20 port 80-wme0hsxg.e6to8jdmiysycbmeepm29nfprvigdwev.top - GET /1dkfJu.php 1dkfJu=wME0HsXGMATTHEW</b>

<br/>
<img src="https://github.com/sdkallullathil/Boleto/blob/584c2fddd88327f6d7d449b441d12b75020463fd/tcpstream.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>
<br/>
<img src="https://github.com/sdkallullathil/Boleto/blob/6c7d4c5110a4432ec20c58f434e048fa682cb28f/download.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>
<br />



In my thorough examination of the pcap, I identified all post-infection traffic, which is as follows:

- 65.181.112.240 port 80 - GET /bibi/w7.txt
- 65.181.112.240 port 80 - GET /bibi/aw7.tiff
- 65.181.112.240 port 80 - GET /bibi/W7.zip
- 65.181.112.240 port 80 - GET /bibi/dll.dll
- 65.181.112.240 port 80 - GET /bibi/dll.dll.exe
- 65.181.112.240 port 80 - www.devyatinskiy.ru - GET /bsb/infects/index.php?[long string]
- 65.181.112.240 port 80 - www.devyatinskiy.ru - GET /bsb/debugnosso/index.php?[long string]
- 158.69.99.213 port 80 - log.houselannister.top - POST /mestre/admin/x.php



<br/>
<img src="https://github.com/sdkallullathil/Boleto/blob/9fbf504b978e596ea53633eb512facad8e1b23f8/packets.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>
<br />

<h2>Crafting Snort Rules for Incident Detection</h2>

In response to the identified Boleto malware incident, a series of carefully crafted Snort rules were developed to generate alerts at various stages of the attack. These rules serve as a proactive defense mechanism, effectively detecting both the initial assault and subsequent occurrences within the network. The following is an overview of the formulated Snort rules, each tailored to target specific indicators of compromise:
<br/>

- Probable Successful Phishing Attack:

<b>alert tcp $HOME_NET any -> $EXTERNAL_NET $HTTP_PORTS (msg:"Probable successful phishing attack."; flow:established,to_server; content:"GET"; http_method; content:"/1dkfJu.php?"; http_uri; classtype:trojan-activity; sid:10000001; rev:1;)</b>

- Probable Post-Infection - Boleto-themed Malicious Spam (First Indicator):

<b>alert tcp $HOME_NET any -> $EXTERNAL_NET $HTTP_PORTS (msg:"Probable post-infection - Boleto-themed malicious spam. First indicator."; flow:established,to_server; content:"GET"; http_method; content:"/bibi/"; http_uri; pcre:"/(\.txt|\.tiff|\.zip|\.dll|\.exe)/U"; classtype:trojan-activity; sid:10000002; rev:1;)</b>

- Probable Post-Infection - Boleto-themed Malicious Spam (Second Indicator):

<b>alert tcp $HOME_NET any -> $EXTERNAL_NET $HTTP_PORTS (msg:"Probable post-infection - Boleto-themed malicious spam. Second indicator."; flow:established,to_server; content:"GET"; http_method; content:"/bsb/infects/index.php?"; http_uri; classtype:trojan-activity; sid:10000003; rev:1;)</b>

- Probable Post-Infection - Boleto-themed Malicious Spam (Third Indicator):

<b>alert tcp $HOME_NET any -> $EXTERNAL_NET $HTTP_PORTS (msg:"Probable post-infection - Boleto-themed malicious spam. Third indicator."; flow:established,to_server; content:"GET"; http_method; content:"/bsb/debugnosso/index.php?"; http_uri; classtype:trojan-activity; sid:10000004; rev:1;)</b>

- Probable Post-Infection - Boleto-themed Malicious Spam (Fourth Indicator):

<b>alert tcp $HOME_NET any -> $EXTERNAL_NET $HTTP_PORTS (msg:"Probable post-infection - Boleto-themed malicious spam. Fourth indicator."; flow:established,to_server; content:"POST"; http_method; content:"/mestre/admin/x.php"; http_uri; classtype:trojan-activity; sid:10000005; rev:1;)</b>

To implement these rules, the command sudo rule-update is executed, ensuring the Snort intrusion detection system is equipped with the latest set of rules for optimal detection and response capabilities.





<h2>Rule Validation and Testing</h2>

To ensure the effectiveness of the meticulously crafted Snort rules, a comprehensive validation process was implemented. The verification involved the replay of the pcap file using tcpreplay, a powerful tool for simulating network traffic. The following steps outline the validation process:<br/></b>
<b>sudo tcpreplay 2016-12-17-traffic-analysis-exercise.pcap.zip -t -i eth1 -l 5 2016-12-17-traffic-analysis-exercise.pcap</b>
<br/><br/>
Explanation of Parameters:<br/><br/>
-t: Enables fast replay mode.<br/>
-i eth1: Specifies the network interface for transmitting the replayed traffic.<br/>
-l 5: Sets the number of loops to 5, allowing for multiple iterations of the pcap replay.<br/>

This process served to replicate real-world conditions, simulating the network activity associated with the Boleto malware incident. By observing the alerts generated by Snort during this simulated attack, we were able to evaluate the rules' responsiveness and accuracy in identifying malicious behaviour.
The validation phase not only ensures the reliability of the Snort rules but also provides valuable insights into their performance under different network conditions. This meticulous testing approach enhances the overall confidence in the rules' capability to effectively detect and respond to potential threats in a dynamic and evolving cybersecurity landscape.



<h2>Visualization with Squert</h2>

In our project, Squert played a key role in understanding the Boleto malware incident. It visualized alerts from Snort, creating a clear timeline to track the attack. Squert's ability to connect alerts helped me to identify patterns in Boleto's tactics. Its user-friendly design made it easy to navigate and quickly access important information. Squert's capabilities empowered analysts to uncover the attack's complexities, significantly improving our cybersecurity defense. Overall, Squert enhanced the visualization of security events, providing valuable insights for an effective response to the Boleto malware threats.




<br/>
<img src="https://github.com/sdkallullathil/Boleto/blob/8dfa7cfa19bea5f0281dd4511ce31e0e7c2f1c94/squert.png" height="90%" width="90%" alt="Disk Sanitization Steps"/>
<br />



<h2>Conclusion</h2>

This project focuses on refining skills in Wireshark PCAP analysis, Snort rule creation, and testing, with a specific emphasis on dissecting the Boleto malware—a notable threat in banking information theft, particularly in Brazil. Operating within the Security Onion virtual machine environment, Wireshark is pivotal for pcap analysis, unveiling insights into Boleto's malicious behavior, while carefully crafted Snort IDS rules act as vigilant guardians to detect potential malware presence.

To validate defensive measures, TCPReply orchestrates the precise pcap rerun, with Squert visually presenting comprehensive logs and alerts, enhancing our understanding and response capabilities in the complex realm of cybersecurity. Beyond technical exploration, this strategic project aims to fortify defenses against the Boleto malware threat. By dissecting its intricacies within the controlled environment of Security Onion, our goal is not only to enhance technical skills but also to contribute meaningfully to the broader field of cybersecurity.
