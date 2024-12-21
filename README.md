# Securing a Cloud-Based Web Application: Azure Deployment and Security Implementation
##### UCI's Cybersecurity Boot Camp Project #1

## OBJECTIVE SUMMARY

The objective of this project was to build, deploy, and secure a web application hosted on Microsoft Azure. The focus was on implementing a range of security measures, including SSL certificates, Web Application Firewalls (WAF), and cloud security configurations, to safeguard the application from common threats. Through this project, I deepened my understanding of cloud security principles, network security, cryptography, and defensive strategies in real-world scenarios.
### CONCISE PROJECT HIGHLIGHTS
Key Achievements:
- Built and hosted a custom web application using Microsoft Azure.
- Implemented SSL encryption with self-signed and managed certificates.
- Secured the application using a Web Application Firewall (WAF) and custom security rules.
- Utilized Azure Security Center to analyze and remediate vulnerabilities.

### TECHNICAL SKILLS LEARNED

- Understanding of Microsoft Azure services: App Service, Key Vault, Front Door, and Security Center.
- Hands-on experience in SSL/TLS implementation and certificate management; Self-signed & App service managed.
- Application of cloud security best practices, including secret management and WAF rule configuration.
- Enhanced skills in networking, cryptography, and terminal-based development.

### TOOLS USED
- <b>Cloud Platform</b>: Microsoft Azure (App Service, Key Vault, Security Center, Front Door)
- <b>Certificate Tools</b>: OpenSSL, CA Root Authority Certificates
- <b>Domain Management</b>: GoDaddy (custom domain: carloncyber.xyz)
- <b>Containerization Framework</b>: Docker


## STEPS TAKEN TO COMPLETE THE PROJECT
### Summary
1. <b>Web Application Setup</b>:
   - Created an Azure web app and hosted it on a custom domain.
   - Deployed a Docker container to host the web application.
   - Designed and customized the web application interface.
2. <b>SSL Encryption Implementation</b>:
   - Created a Key Vault to securely manage secrets and certificates.
   - Generated a self-signed SSL certificate using OpenSSL.
   - Imported and bound the self-signed certificate to the Azure web app.
   - Configured and applied an app service-managed certificate for enhanced security.
3. <b>Advanced Security Features</b>:
   - Configured Azure Front Door to route traffic and improve security.
   - Analyzed and applied Web Application Firewall (WAF) rule sets.
   - Created and tested custom WAF rules to address specific security scenarios.
4. <b>Security Analysis and Optimization</b>:
   - Used Azure Security Center to analyze the security posture of the application.
   - Reviewed and remediated recommendations to align with best practices.
       
### Detailed Steps 
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
   - Step 3: Vist GoDaddy profile and update the DNS records for validation. Under the "Domains" portal, review and update the current DNS records to edit the A record and TXT record with the information that Azure supplied.
       <img width="1105" alt="image" src="https://github.com/user-attachments/assets/b1e6f81c-636a-4622-a41c-47b2f83d17ed">
   - Step 4: Return to Azure and validate the custom domain has been validated, either by readding the custom domain or refreshing the page. 

3) Container Deployment:

   - Explanation: Used the Azure Cloud shell to deploy a containerized application to the web app for a consistent environment.
   - Step 1: Visit the hub.docker container website and use the container cyberxsecurity/project1-apachewebserver container. On the Azure portal, click the Cloud shell icon in the upper right corner and proceed to use the command "az webapp config container set --name <name of your webapp> --resource-group <name of your resource group> --docker-custom-image-name <container-name> --enable-app-service-storage -t", while personalizing the command that is specific to my website. To verify that the container had been added and running correctly, run the command "az webapp config container show --name <name of webapp> --resource-group <name of your resource group>". Here is what should be produced on the webpage as this container is just a template:
        <img width="842" alt="image" src="https://github.com/user-attachments/assets/4873bd94-169d-4a2f-8d48-096d719fa558">

4) Web Application Design:

   - Explanation: Designed and developed the custom web application functionality.
   - Step 1: In order to update the webpage, I needed to SSH into the container. Go to the Web App portal and click on "SSH" in the toolbar. Once the shell opens, I needed to visit the correct directories that contain the html files (/var/ww/html). Using the command, nano index.html, I was able to inspect the html elements and update the container template to my desired information, such as; my name, email address, linkedIn, and two "blog" topics.
        <img width="1052" alt="image" src="https://github.com/user-attachments/assets/ec538196-7a8d-4e79-9081-7aa36414d2ce">
   - Here is the final result of the application design:
        <img width="879" alt="image" src="https://github.com/user-attachments/assets/c1b83402-b878-4613-b8e8-64c143c70ce0">

5) Securing the Application:
   
   a) Key Vault and Certificates:
   - Explanation: Created an Azure Key Vault to securely store cryptographic keys and secrets used by the application.
   - Steps 1: On the Azure portal, search for "Key vaults" and select the "create tab". Under this section, I will be using the preselected subscription group and resource group as using in previous steps. In the configuration steps, under "Access Policies" I will select the USER (Carl) with the predetermined permissions. 

   b) Binding an SSL Certificate:
   - Explanation: Bound the chosen SSL certificate to the web app to enable secure HTTPS communication.
   - Step 1: Now that the Key Vault is created, I will use the Cloud shell and the tool OpenSSL in order to create a self signed certicate by running this command, "  openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout <privatekeyname.key> -out <certificatename.crt> -addext "extendedKeyUsage=serverAuth". After running the command, I needed to fill out several questions about the certificate, such as; Country, State, Organization name, etc... Here is a sample image: 
        <img width="562" alt="image" src="https://github.com/user-attachments/assets/57874a59-27f9-4817-b802-95e45c780793">
   - Step 2: After the certicate is created, I had to create a compatible format so that it is Azure compatible. By using OpenSSL, I created the new PFX format using the command: "openssl pkcs12 -export -out <new_certificatename.pfx> -inkey <keyname.key> -in <certificename.crt>". This new certificate has been added to my web application and now needs to be added to Azure in the PFX format.
   - Step 3: Download the PFX certicate and visit the Azure "Key vaults" portal and select "certificates." From this menu, select "Generate/Import" and complete the certicate questions and upload the PFX cert file.
        <img width="1162" alt="image" src="https://github.com/user-attachments/assets/9c5ebc97-234b-42ee-8e22-4e6f6ca3963a">
   - Step 4: After upload, visit the "Web App" portal and select certicates. This is where I imported the PFX certicate from the key vault.
         ![image](https://github.com/user-attachments/assets/76918aaf-8629-48e5-89b9-f9d739851446)

   - Step 5: After uploading the self-signed certicate, I had to visit the "custom domains" portal and bind my newly uploaded certicate to my domain/webpage. After clicking, "Add binding", the TLS/SSL binding settings required my certificate and TLS/SSL type, which I selcted as SNI SSL. Even after completing this step, my webpage is still not considered secure, so the next step is use Azure and create a "Managed certificate".
   - Step 6: Under the "Web app" portal, I returned back to "Certificates" and clicked on add to create and update my TLS/SSL binding. Under this section, I needed to validate my imported cert and then revisit "Custom domains" to "add binding". This will update my TLS/SSL certificate for my webpage to become secure.
         <img width="1240" alt="image" src="https://github.com/user-attachments/assets/a5adc9a0-5c4a-4aeb-928e-7c564b536d1e">

   c) Web Application Firewall (WAF) on Azure Front Door:
   - Explanation: Configured and analyzed the Web Application Firewall (WAF) rule sets to protect the application from common attacks.
   - Enabled relevant rule sets based on the application's needs.
   - Created custom WAF rules to address specific security concerns.
     - Step 1: Create a WAF for the Azure Front Door by searching on the Azure portal for "Web Application Firewall policies WAF". Under the WAF portal, I selected create and used Regional WAF for the policy group.
     - Step 2: After the WAF resource is created, I analyzed the rule set and saw what vulnerabilities the WAF will protect against.
     - Step 3: Based on the assignment, I created custom rules for the WAF in order to only accept traffic from locations in the United States, Canada, and Australia. This was done by selecting the custom rules in the WAF portal and simply adding the custom rule and configuring an allow list of the three previously stated countries.
          ![image](https://github.com/user-attachments/assets/d94bdf34-c55d-4221-9380-8052aa7c7b30)

   D) Azure Security Center:
   - Explanation: Analyzed recommendations from Azure Security Center to identify and address potential security vulnerabilities.
   - Steps: In order to access and understand the security center recommendations, I revisted the "Web App" portal and selected the "Microsoft Defender for Cloud". This dashboard provided various security recommendations in which I reviewed and prioritized them based on risk, and ultimately implemented remediation steps as needed. Here is a sample screenshot of the dashboard:          ![image](https://github.com/user-attachments/assets/4295a63a-f10f-478b-89e6-3ff088cf2b62)




