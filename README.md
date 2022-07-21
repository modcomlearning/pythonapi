## Python API to Retrieve Products and Make MPESA Payment.
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
### Creating the Database, From the dashboard, click Databases From the TOP BAR, Setup database passwords and Press Initialize, NB: Please save the host, username, password, and database name
### You get into below Page, Here we can see a database with default name i.e yourusername$databasname.


#### Below page appears, 
![q10](https://user-images.githubusercontent.com/66998462/180137168-e04ca2f6-1f21-413a-9d61-b0f33c8e3741.png)

#### Click on the defaul database and a console appears, see below screen. 
![q11](https://user-images.githubusercontent.com/66998462/180137183-447ceab5-3be9-4498-81b8-3b7f6213c4ff.png)

### Step 5
#### After the console finishes loading enter below SQL command to create atable.
```
CREATE TABLE products ( product_name VARCHAR(50), product_desc TEXT, product_cost VARCHAR(50), image_url VARCHAR(200));
```

![q13](https://user-images.githubusercontent.com/66998462/180138307-8b94c980-2966-452d-b452-8ff4f31b8bb7.png)

### Step 6
#### After this Insert a New Record to your products table using below command.
```
insert into  products ( product_name, product_desc, product_cost, image_url) values('Nice Table', 'This is a nice table for your house', '3500', 'https://modcom.co.ke/pics/furniture1.jpeg');
```

![q14](https://user-images.githubusercontent.com/66998462/180138337-0256edea-2789-485a-9b2b-4dd848e355d7.png)


#### You can now use select query to see the table you just created and its data.
![q15](https://user-images.githubusercontent.com/66998462/180138393-79e19e5f-f8ac-47e8-9323-0b927c622f7d.png)

### You are Done Setting up a Database! Add more Records using the Insert Query.


### Step 7
#### We now go to set up our Python Files, From the Dashboard Click on Consoles Menu, From this Page click on Bash
![q16](https://user-images.githubusercontent.com/66998462/180139216-cc7560a1-ebf1-45dc-9f15-e2b2a7150556.png)

![q17](https://user-images.githubusercontent.com/66998462/180139223-195b9c5d-c4b3-41f4-9134-996d0f68e0a1.png)

#### Write below command to install pymysql and flask_cors
```
pip install pymysql

pip install flask_cors

```
![q18](https://user-images.githubusercontent.com/66998462/180139633-1107bb2b-acc4-4112-ab31-ef37f9424254.png)

## Step 8
### Now go to Files Menu. Click on mysite and you will see flask_app.py.
![q19](https://user-images.githubusercontent.com/66998462/180139819-0f08a179-e221-4673-b329-599e47fb808d.png)

![20](https://user-images.githubusercontent.com/66998462/180139889-1074161f-6f9c-4b90-9daa-d82f07b1b21a.png)

#### In this File enter below code and Save.
```
from flask import *
from flask_cors import CORS
import requests
app = Flask(__name__)
CORS(app)
cors = CORS(app, resources={r"/api/*": {"origins": "*"}})
import pymysql

# Your routes
@app.route('/api/all')
def all():
    # Change DB connection to yours
    con = pymysql.connect(host='Modcom.mysql.pythonanywhere-services.com', user='Modcom', password='2491Mod@#$',
                          database='Modcom$cyberdb')
    cursor = con.cursor(pymysql.cursors.DictCursor)
    sql = "select * from products"
    cursor.execute(sql)
    rows = cursor.fetchall()
    return jsonify(rows)




import datetime
import base64
from requests.auth import HTTPBasicAuth
@app.route('/mpesa_payment', methods = ['POST'])
def mpesa_payment():
        #if request.method == 'POST':
            from flask import request
            json = request.json
            amount = json['amount']
            phone = json['phone']
            # GENERATING THE ACCESS TOKEN
            consumer_key = "GTWADFxIpUfDoNikNGqq1C3023evM6UH"
            consumer_secret = "amFbAoUByPV2rM5A"

            api_URL = "https://sandbox.safaricom.co.ke/oauth/v1/generate?grant_type=client_credentials" #AUTH URL
            r = requests.get(api_URL, auth=HTTPBasicAuth(consumer_key, consumer_secret))

            data = r.json()
            access_token = "Bearer" + ' ' + data['access_token']

            #  GETTING THE PASSWORD
            timestamp = datetime.datetime.today().strftime('%Y%m%d%H%M%S')
            passkey = 'bfb279f9aa9bdbcf158e97dd71a467cd2e0c893059b10f78e6b72ada1ed2c919'
            business_short_code = "174379"
            data = business_short_code + passkey + timestamp
            encoded = base64.b64encode(data.encode())
            password = encoded.decode('utf-8')


            # BODY OR PAYLOAD
            payload = {
                "BusinessShortCode": "174379",
                "Password": "{}".format(password),
                "Timestamp": "{}".format(timestamp),
                "TransactionType": "CustomerPayBillOnline",
                "Amount": amount,  # use 1 when testing
                "PartyA": phone,  # change to your number
                "PartyB": "174379",
                "PhoneNumber": phone,
                "CallBackURL": "https://modcom.co.ke/job/confirmation.php",
                "AccountReference": "account",
                "TransactionDesc": "account"
            }

            # POPULAING THE HTTP HEADER
            headers = {
                "Authorization": access_token,
                "Content-Type": "application/json"
            }

            url = "https://sandbox.safaricom.co.ke/mpesa/stkpush/v1/processrequest" #C2B URL

            response = requests.post(url, json=payload, headers=headers)
            print (response.text)
            response = jsonify({"sucess":"Paid {} - {}".format(phone, amount)})
            response.status_code = 200
            return response
 ```
 
 ### NB: Please note you need to change your Database connections.
 You are Done.
 
 ## Step 9
 ### Go to Web Menu and Reload your application, The Green Button
![21](https://user-images.githubusercontent.com/66998462/180140188-feae01c5-4523-4a67-ae18-b7f61d7ec101.png)


### My API is Up on this Link  (https://modcom1.pythonanywhere.com/api/all)

### Looks something Like below

```
[
  {
    "image_url": "https://modcom.co.ke/pics/furniture1.jpeg",
    "product_cost": "3500",
    "product_desc": "This is a nice table for your house",
    "product_name": "Nice Table"
  }
]
```

### Thank you, Glad You Manged to Set Up Your API!
### Please Follow Our Github Repository For More Codes (https://github.com/modcomlearning)

