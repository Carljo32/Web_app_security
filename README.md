# Building and Securing a Web Application via Microsoft Azure

## OBJECTIVE

This project aimed to build, deploy, and secure a web application on Microsoft Azure. The focus was on implementing various security measures to protect the application from common threats and vulnerabilities. This hands-on experience was designed to deepen understanding of network security, cloud security and defensive strategies.

### SKILLS LEARNED

- Understanding of Azure Services: Learned to utilize Azure services like App Service, Key Vault, Front Door, and Security Center.
- Web Application Security: Gained practical experience in securing web applications with SSL certificates (self signed via openssl and CA authority), Web Application Firewall (WAF), and custom WAF rules.
- Security Best Practices: Explored security best practices for cloud deployments, including managing secrets and analyzing security recommendations.
- Development of critical thinking and problem-solving skills in cloud security.
- Updating DNS records; TXT and A records

### TOOLS USED
- Microsoft Azure Portal
- Web development framework (e.g., React, Angular, or ASP.NET) (if applicable)
- Tools for generating self-signed certificates (openssl)
- CA root authority certicate
- Go Daddy domain services (for creating custom domain - carloncyber.xyz)


## STEPS
### Summary
   1. Create an Azure web app
   2. Create a domain
   3. Deploy a container on the web app
   4. Design a custom web app
   5. Create a Key Vault
   6. Create a self-signed certificate
   7. Import and bind a self-signed certificate to a web app
   8. Create and bind an app service managed certificate
   9. Create a front door
   10. Analyze and configure WAF rules
   11. Analyze and remediate security center recommendations
       
### Detailed Steps with Screenshots

1) Azure Web App Creation:

   - Explanation: Created an Azure web app service to host the application.
   - Steps: On the Azure portal, search "App Services" and create the service. For the details section, I used my current subscription service, a previously created Resource Group (RedTeam), and a Runtime stack of PHP 8.2. For the App Service Plan, I used a Linux server and the basic B1 server configurations.
     <img width="1245" alt="image" src="https://github.com/user-attachments/assets/2eab982d-7c66-43ce-8489-2147ff757970">
   

2) Domain Selection and Mapping to Azure:

   - Explanation: Selected a domain name for the web application on GoDaddy.
   - Step 1: Used GoDaddy Domain Service to create and register a custom domain name (carloncyber.xyz).
     ![image](https://github.com/user-attachments/assets/d898a038-86a5-4a4e-b84e-3175ab4bc81c)
   - Step 2: Is to map the custom domain to the current Azure app service. Under the App Services portal, I updated my new custom domain to the "Custom Domain" menu; Selecting the options for Domain Provider as "other domain services", The TLS/SSL certificate as "App Service Managed", and SSl type as "SNI SSL". This is where I added my custom domain as carloncyber.xyz and produced my Domain Validation records.
     <img width="1148" alt="image" src="https://github.com/user-attachments/assets/5db12815-6a86-4489-871e-1cd8bdbc33e8">


3) Container Deployment:

   - Explanation: (If applicable) Deployed a containerized application to the web app for a consistent environment.
   - Steps: Followed Azure instructions for container deployment, specifying the container registry and container image details.

4) Web Application Design:

   - Explanation: Designed and developed the custom web application functionality.
   - Steps: Used a chosen web development framework to build the application locally, test it, and then deploy the code to the Azure web app.

5) Securing the Application:
   
   a) Key Vault and Certificates:
   - Explanation: Created an Azure Key Vault to securely store cryptographic keys and secrets used by the application.
   - Steps: Followed Azure instructions to create a Key Vault and store either a self-signed certificate generated with OpenSSL (for testing) or an app service managed certificate (for production).

   b) Binding an SSL Certificate:
   - Explanation: Bound the chosen SSL certificate to the web app to enable secure HTTPS communication.
   - Steps: Downloaded the certificate from Key Vault and uploaded it to the web app's TLS/SSL settings.

   c) Azure Front Door (Optional):
   - Explanation: (If applicable) Configured an Azure Front Door for a scalable and secure entry point to the application.
   - Steps: Followed Azure instructions to create a Front Door instance and define backend pools and routing rules.

   d) Web Application Firewall (WAF):
   - Explanation: Analyzed and configured the Web Application Firewall (WAF) rule sets to protect the application from common attacks.
   - Enabled relevant rule sets based on the application's needs.
   - Created custom WAF rules to address specific security concerns (optional).

   e) Azure Security Center:
   - Explanation: Analyzed recommendations from Azure Security Center to identify and address potential security vulnerabilities.
   - Steps: Accessed Security Center, reviewed recommendations, prioritized them based on risk, and implemented remediation steps as needed.

Every screenshot should have some text explaining what the screenshot is about.

