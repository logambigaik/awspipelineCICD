# awspipelineCICD  -For code refer (https://github.com/logambigaik/springboo-without-db.git)
# Step1 :create aws-pipeline:

   


![image](https://user-images.githubusercontent.com/54719289/110517075-64884e80-8130-11eb-8d2f-363462c0890b.png)

# Step2 : Add soure stage (Github settings):


![image](https://user-images.githubusercontent.com/54719289/110518081-ac5ba580-8131-11eb-9a33-92a56764b3ae.png)

![image](https://user-images.githubusercontent.com/54719289/110517839-60106580-8131-11eb-9a09-b8c7a6d93692.png)
![image](https://user-images.githubusercontent.com/54719289/110517883-6f8fae80-8131-11eb-8a3f-a38dcf2519ef.png)

   After giving access to github,
  
  ![image](https://user-images.githubusercontent.com/54719289/110518801-97cbdd00-8132-11eb-8690-a44f80154e29.png)

# Step3: Add build stage ( Either add AWS buld or Jenkins):

https://docs.aws.amazon.com/codebuild/latest/userguide/sample-codedeploy.html

      version: 0.2

      phases:
         install:
            runtime-versions:
            java: corretto11
         build:
         commands:
            - echo Build started on `date`
            - mvn test 
         post_build:
         commands:
            - echo Build completed on `date`
            - mvn package
         artifacts:
         files:
         - target/*.jar
         - scripts/*.shh
         - appspec.yml
         discard-paths: yes


![image](https://user-images.githubusercontent.com/54719289/110523470-22fba180-8138-11eb-9f0c-9a86e78a8e7d.png)
![image](https://user-images.githubusercontent.com/54719289/110523538-3eff4300-8138-11eb-9839-8119bb21d748.png)
![image](https://user-images.githubusercontent.com/54719289/110523598-56d6c700-8138-11eb-848a-73fec53c69e6.png)
![image](https://user-images.githubusercontent.com/54719289/110526854-4fb1b800-813c-11eb-8e0c-df1d363a86d6.png)


# Step3 : Code Deploy:

      1. Create EC2 INstance with Add-key Keyname : Name and Value : Codedeploy
  ![image](https://user-images.githubusercontent.com/54719289/110528525-3f024180-813e-11eb-9024-3be00fe47a06.png)   
      2. Create new role for EC2 with S#fullaccess --> rolename: s3fullaccess
   ![image](https://user-images.githubusercontent.com/54719289/110528421-26922700-813e-11eb-9c1e-bc11662a17ca.png)
   
      3. ATtach the role into EC2 instance
   ![image](https://user-images.githubusercontent.com/54719289/110528831-92748f80-813e-11eb-9ed5-8656ef5539f3.png)
   ![image](https://user-images.githubusercontent.com/54719289/110528937-ac15d700-813e-11eb-8bce-e7bd44a896a6.png)


      4. Create  Code Deploy - Application:
![image](https://user-images.githubusercontent.com/54719289/110536778-dcae3e80-8147-11eb-9ce3-7519912eb71a.png)
![image](https://user-images.githubusercontent.com/54719289/110536964-13845480-8148-11eb-85f4-fc683cb329e8.png)

            # Create deployment group
![image](https://user-images.githubusercontent.com/54719289/110537172-55ad9600-8148-11eb-9821-9dcd69d919cc.png)
![image](https://user-images.githubusercontent.com/54719289/110538000-7a563d80-8149-11eb-95ad-ca1ac4a46fc5.png)

![image](https://user-images.githubusercontent.com/54719289/110538354-f8b2df80-8149-11eb-87dd-b44243962872.png)
![image](https://user-images.githubusercontent.com/54719289/110538481-1a13cb80-814a-11eb-81de-f6eb236da3b3.png)


![image](https://user-images.githubusercontent.com/54719289/110539175-ea18f800-814a-11eb-9aa7-72d2a5cfc53f.png)

            # Update Agent on EC2 instnace:
            
![image](https://user-images.githubusercontent.com/54719289/110539343-2187a480-814b-11eb-8180-3c8555761b15.png)

         Install code deploy agent script in EC2 instance:(REfer the link:https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-windows.html)
         
         
![image](https://user-images.githubusercontent.com/54719289/110538141-a5d92800-8149-11eb-9d53-6ab99aed8e65.png)


             1  yum install -y ruby
             2  wget https://aws-codedeploy-eu-west-2.s3.amazonaws.com/latest/install
             3  cd install
             4  chmod +x install
             5  sudo ./install auto
            
            
            # Restart the service codedeploy-agent:
            
               service codedeploy-agent restart
               
  ![image](https://user-images.githubusercontent.com/54719289/110542577-37976400-814f-11eb-8a45-e69e3e4c7ca8.png)
  
         # Now Agent is running in our instance
  
  ![image](https://user-images.githubusercontent.com/54719289/110543016-c99f6c80-814f-11eb-85b9-874df826dfd2.png)


         # If any issue, check the log
         
               /var/log/aws/codedeploy-agent/codedeploy-agent.log
               
          # Disable load balancer and crete deployment group:
          
   ![image](https://user-images.githubusercontent.com/54719289/110543617-8db8d700-8150-11eb-85d4-760cb477b7b2.png)

   ![image](https://user-images.githubusercontent.com/54719289/110543880-e4261580-8150-11eb-8ead-cac9ee4529db.png)
   
   
   ![image](https://user-images.githubusercontent.com/54719289/110830450-3b49f880-82bf-11eb-9cc3-c69772c34c3e.png)


       
  


