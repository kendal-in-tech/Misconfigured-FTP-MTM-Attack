# Misconfigured-FTP-MTM-Attack


![2](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/ad92b26b-6c4b-4297-a41b-2932190081d5)


In this Lab we will discuss FTP, and why and how to use SFTP to secure your FTP communications. We will also perform a MTM Attack, and attempt to access files using the Client PC's login credentials.

What is FTP?

FTP, short for File Transfer Protocol, is like a method for moving files from one computer to another over the internet. Imagine you have a file cabinet in one office (your computer) and you need to send files to a cabinet in another office (another computer, usually a server that stores a lot of data). FTP is one of the ways you can do that. FTP uses Port 21 for communications. 

Here’s how it works:

Two Computers: You have your computer and another computer you want to send files to or get files from.
Connection: Both computers need to be connected to the internet and set up to talk to each other using this method.
Sending and Receiving: You can either send files to the other computer or receive files from it.
Even though there are newer ways to send files using the internet, FTP is still used especially in situations where a lot of files are moved regularly, like in banks or when downloading software from the internet using a web browser.

Think of FTP like a club that normally requires a membership card to enter. However, due to a common setup mistake, there's a "guest pass" available called "anonymous." This guest pass should only allow people into the lobby, but instead, it lets them go anywhere in the club, just like a member. When using the guest pass, you can enter any password, and it will still work. This is risky because it means anyone can get in and access areas they're not supposed to.

We will exploit this misconfiguration is this Lab. This Lab is also available for you to perform yourself using HackTheBox. https://app.hackthebox.com/starting-point


# Recon' & Exploitation 


1. In this Lab we are connected to the same VPN as the Client PC we are attacking. Essentially we are using the tactics of a Insider Threat/Hacker. We want to perform some recon' in order to see if we can reach the target PC. If we can PING the target, for example, we know that we may be able to gather more information by using different tools such as NMAP to discover open ports on the client.

2. PING the Target PC. In this particular instance, the target PC has a IP address of 10.129.117.240


![Screenshot 2024-05-02 160700](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/34114325-5810-4ed6-b9f3-32604c61fe0b)


3. The PING to 10.129.117.240 is successful. The target PC is reachable when connected to the same VPN tunnel. We can now use NMAP to scan the taget PC for further vulnerabilities. 

Nmap is a tool commonly used by those who manage and secure computer networks, such as network administrators, security experts, and ethical hackers. It helps them discover which parts of a network are accessible (known as "ports") and review the security settings for each. Think of it like checking which doors are unlocked in a house and what kind of locks are protecting them.


![Screenshot 2024-05-02 160724](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/8706a3c0-1f09-44cb-a3bb-86af37cf0ec4)


4. We can see that Port 21 is open. We will now look to gather more information. We can use nmap -h, in order to gather more information about what we can do with NMAP. In this particular instance, we will look to gather the version type by using the -sV command alongside NMAP. This now gives us the particular version of FTP being used. 


![Screenshot 2024-05-02 160837](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/cf1e0d72-4ac6-4d5a-9654-20c6c269f39f)


![Screenshot 2024-05-02 160904](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/790c61b5-a4c2-492a-917a-11b22a3862e3)


5. Next we will check to see if FTP is installed on our PC. We will use the command ftp -h, if installed, you will see commands with definitions, basically showing what you can do with NMAP.


![Screenshot 2024-05-02 161343](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/cf058b49-b8ff-491d-a9a1-49d9d27ea377)


6. Attempt to connect to target by using the command: ftp 10.129.117.240.


![Screenshot 2024-05-02 161727](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/f8154e8d-7db8-44e3-9f29-be7daa5e01fc)


7. The prompt should ask for USERNAME. For this lab we are exploiting a misconfiguration that allows a user name ANONYMOUS access via FTP. The ANONYMOUS username can be input when the prompt appears, followed
by any password whatsoever since the service will disregard the password for this specific account.


![Screenshot 2024-05-02 161746](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/b72a8216-bfc2-472b-8762-2e79b2aa35d2)


8. Run ls command in order to see if any files exist.


![Screenshot 2024-05-02 161930](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/6d9aa235-a9f3-4fa5-ac63-f16b1d219f39)


9. Use the GET command in order to get the fla.txt file and download to our PC.


![Screenshot 2024-05-02 162130](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/62fdb302-5be2-47b5-b511-3e7b40e578bf)


10. The flag.txt file is now available on your PC. You have used a misconfigured FTP server, and downloaded a file from a client PC.


![Screenshot 2024-05-02 162247](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/fcf5895c-77c0-4e49-ad87-e8e9ad1ea4e1)


# Prevention


FTP can check user credentials before giving access to files, but there's a risk: someone could intercept and read these files during transfer because they're not encrypted. To prevent this, known as a Man-in-the-Middle Attack, network administrators can secure the data by using SSL/TLS or by sending the FTP data through another secure method called SSH. This adds encryption that only the sender and receiver can decode, making the data safe from interception. When using SSH, the FTP uses a different pathway (port 22 instead of the usual port 21), which helps secure the data further.


![2](https://github.com/kendal-in-tech/Misconfigured-FTP-MTM-Attack/assets/168005414/997467d9-324b-405a-aecb-1c701b9ef1af)












