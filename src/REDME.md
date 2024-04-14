
***********************Flask files ************************************************
1. Create a new env: conda create -n jenkins-env python=3.10 -y
2. Activate our environment: conda activate jenkins-env
3. run flask_app.py file: pip install -r requirements.txt
4. write code under main.py file
5. run your main.py file

Test the FASTAPI

{
  "Gender": "Male",
  "Married": "No",
  "Dependents": "2",
  "Education": "Graduate",
  "Self_Employed": "No",
  "ApplicantIncome": 5849,
  "CoapplicantIncome": 0,
  "LoanAmount": 1000,
  "Loan_Amount_Term": 1,
  "Credit_History": "1.0",
  "Property_Area": "Rural"
}



docker build -t loan_pred:v1 .
docker build -t shivan1118/cicd:latest .
docker push shivan1118/cicd:latest
docker run -d -it --name modelv1 -p 8005:8005 shivan1118/cicd:latest bash
docker ps
docker exec modelv1 python prediction_model/training_pipeline.py
docker exec modelv1 pytest -v --junitxml TestResults.xml --cache-clear
docker cp modelv1:/code/src/TestResults.xml .

# Optional
docker exec -d -w /code modelv1 python main.py
docker exec -d -w /code modelv1 uvicorn main:app --proxy-headers --host 0.0.0.0 --port 8085

#changes