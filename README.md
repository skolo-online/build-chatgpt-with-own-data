# flask-app-template
Starting template for a python Flask application

Check out out [YouTube Channel here](https://www.youtube.com/c/SkoloOnline)

## Pull the repo

## Set up the project
Start by installing virtual environment if you do not already have it.

```sh
sudo -H pip3 install --upgrade pip

sudo -H pip3 install virtualenv
```

Create and activate the virtual environment

```sh
virtualenv chatgptenv
souce chatgptenv/bin/activate
```

## Create a folder called data
Save your PDF files in there, note this project will only work with PDF files. Watch the video to see how you can customise the code for othe rinput types. 

## Install required python packages

```sh
pip install Flask
pip install openai
pip install numpy==1.24.2
pip install openai==0.27.1
pip install pandas==1.5.3
pip install redis==4.5.1
pip install requests==2.28.2
pip install ipykernel
pip install textract
pip install tiktoken
```

## Instal Redis Stack Server
In your Ubuntu Virtual server
```sh
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list
sudo apt-get update
sudo apt-get install redis-stack-server
```

### Check Redis Stack Server Installation
```sh
sudo systemctl status redis-stack-server
```

## Check that there is document in the index
Run this line inside of a python shell to check that the index was created successfully, and there are documents in the index

```py
#RUN THIS TEST FUNCTION
redis_client.ft(INDEX_NAME).info()['num_docs']
```


You should get this output:
```sh
● redis-stack-server.service - Redis stack server
     Loaded: loaded (/etc/systemd/system/redis-stack-server.service; enabled; vendor preset: ......
     Active: active (running) since Fri 2023-04-21 13:45:42 CEST; 20h ago
       Docs: https://redis.io/
   Main PID: 365056 (redis-server)
      Tasks: 17 (limit: 2282)
     Memory: 195.0M
     CGroup: /system.slice/redis-stack-server.service
             └─365056 /opt/redis-stack/bin/redis-server *:6379
````

