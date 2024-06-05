# High Availability WordPress on Amazon Lightsail

This document provides detailed step-by-step instructions to set up two Amazon Lightsail instances running WordPress and connect them to a Load Balancer for high availability and fault tolerance.

## Step 1: Set Up Amazon Lightsail Instances

1. **Create Lightsail Account:**
   - If you don’t already have an AWS account, sign up at [AWS Lightsail](https://lightsail.aws.amazon.com/).

2. **Create Two WordPress Instances:**
   - Go to the Lightsail console.
   - Click on "Create instance".
   - Choose the instance location (e.g., closest to your target audience).
   - Select "Linux/Unix" as the platform.
   - Choose "WordPress" as the blueprint.
   - Choose your instance plan (based on your requirements).
   - Name your instance (e.g., `wordpress-1`).
  
![Screenshot 2024-06-04 165757](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/a6f1dc2d-4a28-4505-ba41-32aa243cbe03)
     
![Screenshot 2024-06-04 165817](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/21f73f49-44e6-4292-9642-304b765b92a7)

![Screenshot 2024-06-04 165835](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/9362719a-6a93-4513-bc40-c940c1389ffe)

![Screenshot 2024-06-04 165906](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/0a6841ac-7e51-4e01-ab50-2dcf86a666d5)

   - Repeat the process to create a second instance (e.g., `wordpress-2`).

## Step 2: Configure WordPress Instances

1. **Access Instances:**
   - Go to the Lightsail console.
   - Click on your instance and use the browser-based SSH to connect.

    ![Screenshot 2024-06-04 181740](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/0734e404-804d-4ed5-9f44-f27f35b64811)


2. **Set Up WordPress:**
   - Follow the prompts to complete the initial WordPress setup.
   - Ensure both instances are properly configured and running.

## Step 3: Set Up the Load Balancer

1. **Create a Load Balancer:**
   - In the Lightsail console, go to "Networking".
   - Click on "Create Load Balancer".
   - Name your Load Balancer (e.g., `wordpress-lb`).
   - Choose the appropriate region (same as your instances).
   - Click "Create".
  
    ![Screenshot 2024-06-04 181928](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/7c0caa49-26ea-475f-bd17-308835cad800)

    ![Screenshot 2024-06-04 211446](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/01ed5746-a2d9-413e-84b6-7b2abd1e6633)


1. **Attach Instances to Load Balancer:**
   - After the Load Balancer is created, go to its management page.
   - Click on "Targets" and then "Attach instance".
   - Select your two WordPress instances and attach them.
  
     ![Screenshot 2024-06-04 211717](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/67a76d2b-6be2-4e7b-8247-0ede64486e68)


## Step 5: Enable SSL (HTTPS)

1. **Request an SSL/TLS Certificate:**
   - In the Lightsail console, go to your Load Balancer's management page.
   - Click on the "SSL/TLS" tab.
   -  Request a new certificate: Enter your domain name.
   -  Add any additional domain names if needed (e.g., www.yourdomain.com) and follow the prompts to validate your domain.

   ![Screenshot 2024-06-04 212229](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/4d790859-1b68-4e77-8f6f-151fb1815aee)

   ![Screenshot 2024-06-04 212706](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/e5e0258d-abba-4549-b0ca-9ee615c6f373)

2. **Point Your Domain to the Load Balancer:**
- Get the DNS Name of the Load Balancer
- In the Lightsail console, navigate to your load balancer's management page.
- Copy the DNS name of the load balancer.
- Update Your Domain's DNS Settings Using Amazon Lightsail's Domains and DNS Service

**Navigate to the Networking tab in the Lightsail console.**
- Click on "Create DNS zone".
- Enter your domain name and click "Create DNS zone".

  ![Screenshot 2024-06-04 212752](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/03218207-3d81-4dfc-a87d-fec17e5608d4)

  ![Screenshot 2024-06-04 213303](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/0caa6135-3ba6-424c-b52e-8ee6c1017b77)



## Step 6: Configure DNS for Custom Domain

1. **Get the Load Balancer's DNS Name:**
   - In the Lightsail console, go to the Load Balancer page.
   - Copy the DNS name of your Load Balancer.

2. **Update DNS Records with Your Provider:**
   - Log in to your domain registrar (e.g., GoDaddy, Namecheap).
   - Go to the DNS management page.
   - Find the DNS or Nameserver settings for your domain.
   - Replace the current nameservers with the ones provided by Lightsail. You can find these in the "DNS zone" management page under "Nameservers".
   - Save the changes.
  
     ![Screenshot 2024-06-04 213332](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/44af4d18-7aeb-4628-a7ec-dcad4594006a)

     ![Screenshot 2024-06-04 214239](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/0556572c-d2e4-4c21-af1a-d9f951a77ee1)


## Step 7: Test and Verify

1. **Access Your Website:**
   - Visit your domain name in a web browser.
   - You should see your WordPress site loading through the Load Balancer.

2. **Verify Load Balancing:**
   - To test load balancing, you can temporarily shut down one instance and see if the site remains accessible.
  
     https://shivampatel.in/ 
     ![Screenshot 2024-06-05 031941](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/e3694751-06f5-4941-a614-a680de1b34f8)

     https://info.shivampatel.in/ 
     ![Screenshot 2024-06-05 032007](https://github.com/shivxm03/Amazon-Lightsail/assets/157244434/ed22b701-e915-4377-98cf-84e36ae6fd0e)


By following these steps, you will have a robust setup with two WordPress instances behind a Load Balancer, ensuring high availability and fault tolerance for your website, and using a custom domain name managed by an external DNS provider.
