## Deployment: Lecture 06

- Model deployment is critical as it brings out the flaws and issues in the model and helps in evaluation of the model. 
- With offline evaluation its easy to miss the subtle issues with the model
- Only when the model is deployed that we see if it works well in real-time, ie when it starts interacting with the users or when it starts utilizing real world data.

The mantra for a deployment is 

**Deploy early, deploy often**

**Keep it simple, and add complexity later**

Flow of a model deployment:

- Build a prototype to interact with
- Separate model from UI
- Then scale 
- consider moving the model to edge when speed is essential



#### Step 1: **Building prototype to interact with **

- Huggingface playground
- Gradio
- Streamlit

##### **Best Practices** 

- Have a basic UI

  to get feedback from your colleagues and friends

  - Gradio and Streamlit (slightly complex but more flexible)

- Put it behind a web URL

  - cloud versions of Streamlit and Huggingface are useful

- Just spend a day on i

##### :x: Cons:

- limited front-end flexibility

- doesn't scale to concurrent requests and the model becomes the bottleneck

**Model-in-service approach** is used by Streamlit and Gradio

the same web service is used to run your model and run your service

:heavy_check_mark:**Pros**: reuses existing infrastructure

:x:**Cons**: Large models eat into resources of the web-server, server hardware not optimized for ML workloads, model and server scale differently, models change more frequently than server code, different language of model and server code



#### Step 2: Separate Model from UI

1. ##### Batch Prediction

   - Periodically run model on new data and save the results in a database

     for e.g.  new flyers come in every week and run the model on that data and store the results in the db

   - This is possible in cases where there are relatively less inputs like

     for eg. 1 prediction per user : recommender system

     **Data processing/work flow tools work well here**

     - Run preprocessing
     - load the model
     - run predictions
     - store predictions

     tools: Dagster, Airflow, AWS Step Functions, Perfect, Metaflow

     :heavy_check_mark:**Pros**: simple to implement, scales easily, used in production by large scale production systems for years, fast to retrieve

     :x:**Cons**: Doesn't scale to complex input types, users don't get the most up-to-date predictions, models can frequently become stale

     for e.g. in a recommender system the model will not be able to take into account all the context that the user has provided between the predictions to serve them with updated recommendations

     

2. #####   **Model-as-a Service**

   Model is run as its own service separately. Where the service will interact with the backend or the client 

   by responding to the requests.

   :heavy_check_mark:**Pros**:

   **Dependability** model bugs will not crash the whole web-application, 

   **Scalability**: choose hardware optimal for the model

   **Flexibility:** model can be reused for multiple applications

   :x: **Cons**:

   **Latency**: adds latency to the application

   **Complexity**: adds additional complexity to the application

   

   :arrow_right:  **REST APIs**

   serve predictions to canonically-formed HTTP requests. Alternatives are <u>GRPC</u> (with Tensorflow Serving) and <u>GraphQL</u>

   **No Industry Standard on Rest API for ML services** 

   There is no current standard for formatting requests and responses for Rest API calls. Different cloud services have a different approach how the Rest API is structured.

   - Google Cloud expects a batch of inputs structured as a list called instances
   - Azure and AWS also have a different structure.

   **:arrow_right:Dependency Management for model servers**

   Model predictions depend on code, model weights and dependencies all need to be present on your web server.

   Dependency cause trouble

   **Two Strategies**

   - *CONSTRAIN THE DEPENDENCY OF YOUR MODEL*

      ONNX : standard neural network format

     define network in any language and run it consistently anywhere

     :x: **Cons:**

     - libraries change quickly and often bugs in translation code
     - if there is some codel pre-processing, using python code, outside the ML framework then ONNX cannot handle it

   - *CONTAINERS*(i.e Docker):heavy_check_mark:

     Dockers vs. VM: 

     VMs package the entire OS as well as the libraries and applications that are built on top of that OS

     A container like Docker removes that need by packaging the applications and libraries together

     - Common pattern is to spin up a docker container for every discrete task

     - Docker containers are created from [Docker files](https://docs.docker.com/engine/reference/builder/)

       Docker file runs a sequence of steps to define the environment where the code will run

     Docker has three [components](https://docs.docker.com/get-started/overview/)

     1. docker client : this is the primary way in which you interact with Docker. When commands such as `docker run` etc are used the client sends these commands to `dockerd`i.e the docker daemon. The `docker` command uses the Docker API.
     2. docker daemon: These commands are executed by a **Docker Host**, which can run on either your laptop or your server (with more storage or more performance).
     3. docker registry: the docker host talks to the registry where all the container you want are stored

     :arrow_forward: Other that docker there are few open source packages to containrize and serve ML models like 

     [Cog](https://github.com/replicate/cog), [BentoML](https://github.com/bentoml/BentoML) and [Truss](https://github.com/trussworks)

     They have standard way of defining the prediction service and a other is a YAML file the defines other dependencies and package versions that will go into Docker containers running on your laptop

     

     



​		











