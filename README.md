pip install boto3

import boto3

client = boto3.client(
    "sagemaker-runtime",
    region_name="ap-south-1",
    aws_access_key_id="AKIA55PG63ZQNLNZHR6E",
    aws_secret_access_key="PZoZht+CW1QLvBLCA9evRFsC4pwJ/x50UL+8t2hj"
)

endpoint_name = "xgboost-bank-model-endpoint-20260324055551"

# 🔥 Use sample input
payload = "1,999,0,1,0,0,0,0,1,0,0,0,0,0,0,0,0,0,1,0,0,1,0,0,0,0,0,0,0,1,0,0,1,0,0,1,0,0,0,1,0,0,0,0,0,0,1,0,0,0,0,1,0,0,0,0,1,0,1"

response = client.invoke_endpoint(
    EndpointName=endpoint_name,
    ContentType="text/csv",
    Body=payload
)

result = response["Body"].read().decode("utf-8")
print("Prediction:", result)
