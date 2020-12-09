### Create Layer Lambbda for SAP PyrFC

1) Download SAP NW RFC SDK 7.50 from SAP Marketplace (version for LINUX ON X86_64 64 BIT). Unzip on some route, it will be used in following steps.

2) In this case we will use an AWS Cloud9 environment based on Amazon Linux 2 to generate Layer. A step-by-step guide on how to launch Cloud9 environments in the following link: https://docs.aws.amazon.com/cloud9/latest/user-guide/create-environment-main.html

3) Within the Cloud9 environment, select Window->New Terminal and run the following shell commands to create Python environment and install required dependencies:

```console
sudo yum install -y amazon-linux-extras
sudo amazon-linux-extras enable python3.8
sudo yum install python3.8 -y
virtualenv -p /usr/bin/python3.8 PyRFC_Layer
source PyRFC_Layer/bin/activate
cd PyRFC_Layer
mkdir python
cd python
pip3 install https://github.com/SAP/PyRFC/releases/download/2.1.0/pynwrfc-2.1.0-cp38-cp38-linux_x86_64.whl -t .
cp /usr/lib64/libuuid.so.1 /home/ec2-user/environment/PyRFC_Layer/lib
```

4) Copy from the resulting folder in step 1 all the files in the LIB subfolder to PyrFC_Layer/Lib/ in Cloud9 (dragging and dropping):

![](images/Lambda_Layer_PyRFC_ES/2020-11-20T19-35-32.png)

![](images/Lambda_Layer_PyRFC_ES/2020-11-20T19-37-02.png)


5) Again open console as step 3 and run the following commands, replaced <nombre_bucket> with the target S3 bucket where to store Layer:

```console
cd /home/ec2-user/environment/PyRFC_Layer
zip -r9 pyrfc_layer.zip python lib
aws s3 cp pyrfc_layer.zip s3://<nombre_bucket>/pyrfc_layer.zip
```

6) In the AWS console, enter Lambda service, select Additional Resources->Layers->Create layer.

7) Enter some S3 name and path indicated above (modified <nombre_bucket>) and Python 3.8 compatible Runtime:

![](images/Lambda_Layer_PyRFC_ES/2020-11-20T19-45-39.png)

8) After successfully creating Layer, it can already be used in Lambda. The following is an example code for invoking ABAP demo function:

```python
import json
from pyrfc import Connection

def lambda_handler(event, context):

    con = Connection(ashost='<IP_SAP_AS_ABAP>', sysnr='<NUMERO_SISTEMA>', client='<MANDANTE>', user='<USUARIO>', passwd='<PASSWORD>')
    resultado = con.call('STFC_CONNECTION', REQUTEXT=u'Hola SAP!')

    print (resultado)  

    return {
        'statusCode': 200,
        'body': json.dumps('Conectado con SAP!')
    }
```
