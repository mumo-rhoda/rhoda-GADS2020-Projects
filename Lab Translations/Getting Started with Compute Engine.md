# LAB: Google Cloud Fundamentals: Getting started with Compute Engine.

## OBJECTIVES
  In this lab, you will learn how to perform the following tasks:

    i.  Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
    ii. Create a Compute Engine virtual machine using the gcloud command-line interface.
    iii.Connect between the two instances.

## Steps:
1. Create a compute engine virtual machine using the Google Cloud Platform (GCP) Console.

    gcloud beta compute  instances create my-vm-1 --zone=us-central1-a --machine-type=n1-standard-1 --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE 
     --tags=http-server 
     --image=debian-9-stretch-v20200902 
     --image-project=debian-cloud 
     --boot-disk-size=10GB 
     --boot-disk-type=pd-standard 
     --boot-disk-device-name=my-vm-1 
     --reservation-affinity=any

    gcloud compute firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server


2. Create a compute engine virtual machine using the gcloud command line interface
 # To set your default zone to the one you just chose, enter this partial command:
    gcloud config set compute/zone us-central1-b

 # To create a VM instance called my-vm-2 in that zone, execute this command:
    gcloud compute instances create "my-vm-2" \
    --machine-type "n1-standard-1" \
    --image-project "debian-cloud" \
    --image "debian-9-stretch-v20190213" \
    --subnet "default"

## Note: The VM can take about two minutes to launch and be fully available for use.

3. Connect between the two instances
    # Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
        connect to my-vm-2 :
                gcloud compute ssh my-vm-2
        ping my-vm-1 from my -vm-2:
                ping -c 4 my-vm-1
    
   # Use the ssh command to open a command prompt on my-vm-1 from  my-vm-2:
            ssh my-vm-1

    # At the command prompt on my-vm-1, install the Nginx web server:

        sudo apt-get install nginx-light -y

    # Use the nano text editor to add a custom message to the home page of the web server:

        sudo nano /var/www/html/index.nginx-debian.html

    # Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:

        Hi from YOUR_NAME

    # Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.

    # Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:

        curl http://localhost/

    # The response will be the HTML source of the web server's home page, including your line of custom text.

    # To exit the command prompt on my-vm-1, execute this command:

        exit

    # You will return to the command prompt on my-vm-2

    # To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:

        curl http://my-vm-1/

    # The response will again be the HTML source of the web server's home page, including your line of custom text.

    # To get the external ip of my-vm-1 instance use this command:

            gcloud compute instances list --zones us central1-a
        
   -Copy the External IP address for my-vm-1 and paste it into the address bar of a new browser tab. You will see your web server's home page, including your custom text


# Congratulations!
# In this lab, you created compute engine virtual machine (VM) instances in two different zones and connected to them using ping, ssh, and HTTP.

# End of the Lab