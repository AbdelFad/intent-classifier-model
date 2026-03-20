# Model Deployment and Model Serving

## Intent Classifier Model

This small project demonstrates:

Training a tiny text classifier.
Saving the model artifact.
Serving predictions via a Flask API (/predict).

### Quick start (local)

1. Create a virtualenv and install: 

```sh
python3 -m venv .venv 

source .venv/bin/activate 

pip install -r requirements.txt
```

2. Train the model: 

```sh
python model/train.py #This will create model/artifacts/intent_model.pkl.

```

3. Run the API: 

```sh
python app.py #The API will be available at http://127.0.0.1:6000
```

4. Example request: 

```sh
curl -X POST http://127.0.0.1:6000/predict -H "Content-Type: application/json" -d '{"text":"I want to cancel my subscription"}'

#Response: 

{ 
  "intent": "complaint", 
  "probabilities": {"complaint": 0.85, "question": 0.05, ...} 
}
```

====
# Model Deployment and Model Serving using Virtual Machines

- VPC: Virtual 

- WSGI: Web server Gateway Interface

- ASG : Dynamic scaling --> 

- LB: LoadBalancer --> TG --> ASG


## Architecture:

Internet (client) --> IGW(Internet Gateway) attached to VPC ==>

==> App Load Balancer (ALB) --> internet-facing (Listener: HTTP 80) ==>

==> Target Group (HTTP:80, Health-check:/predict) ==>

==> Auto Scaling Group (ASG) ==>

==> EC2 Instance or GCE (in a Public Subnet) --> Nginx (listen:80) -->Proxy_pass-->Gunicorn(127.0.0.1:6000)-->WSGI app(/predict)

## Note go to git branch virtual-machine