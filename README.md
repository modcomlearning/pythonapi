## Python API to Retrieve Products and Nake MPESA Payment.
### In this session we are creating an API to used by an Android Mobile App check the Mobile App that uses this API on this link
(https://github.com/modcomlearning/shop) <br/>

## Step 1
### Please create an Account on (https://www.pythonanywhere.com/login/)
![q1](https://user-images.githubusercontent.com/66998462/180134900-2e47d97c-ecca-4edc-a243-7c24aa93aa90.png)

## Step 2
### Once You have an Account please Login to access your Dashboard.
![q2](https://user-images.githubusercontent.com/66998462/180135008-d7490e7d-0e87-4d8c-8c6e-8a72039e9eaf.png)

#### On above dashboard please click on Web From Main Menu Links at the Top, You will get a screen like below
![q3](https://user-images.githubusercontent.com/66998462/180135159-d1099bc4-aaa9-4a25-91d0-a9d6dc2109d9.png)

### Step 3
### Click on 'Add A New Web App' from the left side.
#### Please Follow the steps as shown in below screenshots until you create a web App.

#### Next
![q3](https://user-images.githubusercontent.com/66998462/180135489-52a86e5d-57c2-46ac-a678-78972ff1583a.png) <br/>

#### Next
![q4](https://user-images.githubusercontent.com/66998462/180135493-01cdb7ef-105e-4e35-9d8c-50c3cdcc39d1.png)<br/>

 #### Select Flask
![q5](https://user-images.githubusercontent.com/66998462/180135494-6a8a5e79-3987-43e6-8a51-b8f2e55064cd.png)<br/>

 #### Select Python 3.9
![q6](https://user-images.githubusercontent.com/66998462/180135498-426d89ac-da07-460e-8e47-ecbf3f93b6ec.png)<br/>

 #### Next
![q7](https://user-images.githubusercontent.com/66998462/180135502-02864512-e8bc-4f94-87d0-d706f6b281e7.png)<br/>

#### Next
![q8](https://user-images.githubusercontent.com/66998462/180135505-8a739497-837b-4fe9-8784-3d214e03f331.png)<br/><br/>

#### NB: on above screen please see the link of your API. in my case (modcom1.pythonanywhere.com), this page will also help to be reloading our Page.

### Step 4
### Creating the Database, From the dashboard, click Databases From the TOP BAR, Setup database passwords and Press Initialize, You get into below Page, Here we can see a database with default name i.e yourusername$databasname.

#### Below page appears, 
![q10](https://user-images.githubusercontent.com/66998462/180137168-e04ca2f6-1f21-413a-9d61-b0f33c8e3741.png)

#### Click on the defaul database and a console appears, see below screen. 
![q11](https://user-images.githubusercontent.com/66998462/180137183-447ceab5-3be9-4498-81b8-3b7f6213c4ff.png)

#### After the console finishes loading enter below SQL command to create atable.
```
CREATE TABLE products ( product_name VARCHAR(50), product_desc TEXT, product_cost VARCHAR(50), image_url VARCHAR(200));

![q13](https://user-images.githubusercontent.com/66998462/180138307-8b94c980-2966-452d-b452-8ff4f31b8bb7.png)


#### After this Insert a New Record to your products table using below command.
```
insert into  products ( product_name, product_desc, product_cost, image_url) values('Nice Table', 'This is a nice table for your house', '3500', 'https://modcom.co.ke/pics/	furniture1.jpeg');

![q14](https://user-images.githubusercontent.com/66998462/180138337-0256edea-2789-485a-9b2b-4dd848e355d7.png)

You can now use select query to see the table you just created and its data.
![q15](https://user-images.githubusercontent.com/66998462/180138393-79e19e5f-f8ac-47e8-9323-0b927c622f7d.png)






