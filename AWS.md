# AWS

## Access localhost from anywhere using EC2 (ssh remote port forwarding)

Your app's development server runs on https://localhost:8080 and you need to access it from a service somewhere outside in the internet. 

(If your app runs on https, don't use ngrok.com or pagekite.net, they can handle only http.)

* Start EC2 instance, nano is enough. Choose `Auto-assign Public IP`: `Enable`. No need for a (permanent) Elastic IP.
* Edit it's `Security Group`, add a new `Inboud Rule`:

      Custom TCP     8080   Custom     0.0.0.0/0
    
  (Another one will be probably added automatically: `Custom TCP     8080   Custom     ::/0`.)
    
* Connect to your EC2 instance:
     
      ssh -i "your-key.pem" ubuntu@ec2-12-345-678-901.compute-1.amazonaws.com
     
* Edit `sudo vim /etc/ssh/sshd_config`, add this line:  

      GatewayPorts yes
     
* Restart ssh:

      sudo /etc/init.d/ssh restart

* On localhost, forward the port to EC2:

      ssh -R 8080:localhost:8080 -i "your-key.pem" ubuntu@ec2-12-345-678-901.compute-1.amazonaws.com
    
*Troubleshooting*

* What ports are open:

      sudo netstat -ntlp | grep LISTEN
