### MLFlow End to End Tutorial
---
![](https://databricks.com/wp-content/uploads/2018/06/mlflow.png)

### **What is MLFlow?**
---
* **MLflow** is opensource platform to Manage the ML Life Cycle. 
* It includes **experimentation, reproducibility, deployment and central model registry.**
* Advantage of Use **MLFlow** is **Transparency** and **Standardization**.
* It helps you to **train, reuse** and **deploy the model**.

![](https://databricks.com/wp-content/uploads/2020/06/blog-mlflow-model-1.png)

### MLFlow Setup
---
1. Installation of **MLflow**.

```bash
pip install mlflow
```

2. Once you will install with this now time to setup **Central Repository Database** where we will log all our tracking information and also will create the artifacts folder to store our models and its relevant information.

```bash
# Terminal Command
mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./artifacts --host 0.0.0.0 
```
or
```bash
mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./artifacts --host 127.0.0.1 --port 5000
```
![](https://raw.githubusercontent.com/ashishpatel26/MLflow_End_to_End_Example/main/images/step1.jpg)

> **Output**

![](https://raw.githubusercontent.com/ashishpatel26/MLflow_End_to_End_Example/main/images/step1_result.jpg)

> This Command create the **`mlflow.db`** and **`artifacts`** folder.

### Open MLFLOW UI

---

```bash
mlflow ui
```

![](https://raw.githubusercontent.com/ashishpatel26/MLflow_End_to_End_Example/main/images/open_mlflow.jpg)

### MLFLOW UI LOOKS LIKE

---

![](https://raw.githubusercontent.com/ashishpatel26/MLflow_End_to_End_Example/main/images/mlflowui.jpg)

### MLflow Tracking
---
* **MLflow** Tracking is an **API** and **UI** for **Logging Parameter, Code Versions, Metrics, and Output files.**

##### Set Tracking URI and Create Experiment

* We have to create the notebook for tracking server will run in. and we have to set the tracking URI. In our example, `localost:5000` is the tracking URI but you can setup any other tracking host and port in the `set_tracking_uri` function call. 
* Initially we have to default experiment created which you can get with `get_experiment` function call.

⭐ **`mlflow.py`**

---

```python
experiment_id = mlflow.create_experiment("my_experiment")
experiment = mlflow.get_experiment(experiment_id)
```

```python
mlflow.set_tracking_uri("http://localhost:5000")
experiment = mlflow.get_experiment('0')
print("Name: {}".format(experiment.name))
print("Artifact Location: {}".format(experiment.artifact_location))
print("Life Cycle Stage: {}".format(experiment.lifecycle_stage))
print("Experiement ID: {}".format(experiment.experiment_id))
```
### **🤝 Prepare the Notebook with ML Case study**

---
> For Experiment Run Notebook, we have to create the notebook with the following steps.

| Notebook | Link |
|--|:--:|
|Notebook| [Open](Notebook.ipynb)|

**Notebook Flow**

---

![](https://raw.githubusercontent.com/ashishpatel26/MLflow_End_to_End_Example/main/images/flow.png)

### MLFlow Model Flavors

---

> The model can be used with tools that support either the `sklearn` or `python_function` model flavors.

![](https://miro.medium.com/max/700/1*_RIJnhAi-Lpbith39-gRjg.png)

### Diverse Platform

---

> MLflow provides tools to deploy many common model types to diverse platforms.

![](https://miro.medium.com/max/700/1*ZUYhQ-lKlWRiwLFYHMTfcw.png)



### Experiments

---

![](https://raw.githubusercontent.com/ashishpatel26/MLflow_End_to_End_Example/main/images/experiments.jpg)

### Final Model Prediction from Staging Code

---

```python
# Predict with MLflow Model
print("Predict with MLflow Model:")
# models:///XGBoost_Model/{Stage} -- Stage Contains Two Stage 1. Staging 2. Production(Current)
model = mlflow.xgboost.load_model("models:///XGBoost_Model/Production")
print("="*50)
print("Model:\n", model)
print("="*50)
prediction = model.predict(X_test)
# print("Prediction.type:", type(prediction))
# print("="*50)
# print("Prediction.shape:", prediction.shape)
# print("="*50)
print("Prediction:\n", prediction)
print("Prediction Done.")
```

---

### Thanks for Reading 👨‍💻👩‍💻🧑‍💻
