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

## Install required python packages

```sh
pip install Flask
pip install openai
```


## Check Redis Stack Server Installation
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




<script>
$("#gpt-button").click(function(){
  var question  = $("#chat-input").val();

  let html_data = '';
  html_data += `<a href="#" class="list-group-item list-group-item-action d-flex gap-3 py-3">
    <img src="{{ url_for('static', filename='images/favicon.png') }}" alt="twbs" width="32" height="32" class="rounded-circle flex-shrink-0">
    <div class="d-flex gap-2 w-100 justify-content-between">
      <div>
        <p class="mb-0 opacity-75">${question}</p>
      </div>
    </div>
  </a>`

  $('#list-group').append(html_data);
  $("#chat-input").val('');

  //Make the AJAX Call to Server
  $.ajax({
      type: "POST",
      url: "/",
      data: {'prompt': question },
      success: function (data) {
        let gpt_data = '';
        gpt_data += `<a href="#" class="list-group-item list-group-item-action d-flex gap-3 py-3">
          <img src="https://digital-practice.ams3.cdn.digitaloceanspaces.com/static%2Fapp%2Fimg%2Fopenai-logo.png" alt="twbs" width="32" height="32" class="rounded-circle flex-shrink-0">
          <div class="d-flex gap-2 w-100 justify-content-between">
            <div>
              <p class="mb-0 opacity-75">${data.answer}</p>
            </div>
          </div>
        </a>`
        $('#list-group').append(gpt_data);
      }
    });

  });



</script>


if request.method == 'POST':
      prompt = request.form['prompt']

      answer = aiapi.returnChatGPT(prompt)

      data = {}
      data['answer'] = answer
      return jsonify(data), 200



      import openai
      import config

      api_key = config.DevelopmentConfig.OPENAI_KEY
      openai.api_key = api_key


      def returnChatGPT(prompt):
          messages = []
          messages.append({"role": "system", "content": "You are a helpful chat assistant."})

          instruction = {}
          instruction['role'] = 'user'
          instruction['content'] = prompt
          messages.append(instruction)

          res = openai.ChatCompletion.create(model="gpt-3.5-turbo",messages=messages)
          try:
              ans = res['choices'][0]['message']['content'].replace('\n','<br>')
          except:
              ans = 'Sorry, you beat the ChatGPT today, try another question'
          return ans
