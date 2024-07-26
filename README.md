# Cloud-Data-Encryption-Key-Management-and-Data-Privacy-
# open command prompt
Microsoft Windows [Version 10.0.22000.2538]
(c) Microsoft Corporation. All rights reserved.

C:\Users\Student.MAT-42.000>pip install awscli
Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: awscli in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (1.33.27)
Requirement already satisfied: botocore==1.34.145 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from awscli) (1.34.145)
Requirement already satisfied: docutils<0.17,>=0.10 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from awscli) (0.16)
Requirement already satisfied: s3transfer<0.11.0,>=0.10.0 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from awscli) (0.10.2)
Requirement already satisfied: PyYAML<6.1,>=3.10 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from awscli) (6.0.1)
Requirement already satisfied: colorama<0.4.7,>=0.2.5 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from awscli) (0.4.6)
Requirement already satisfied: rsa<4.8,>=3.1.2 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from awscli) (4.7.2)
Requirement already satisfied: jmespath<2.0.0,>=0.7.1 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from botocore==1.34.145->awscli) (1.0.1)
Requirement already satisfied: python-dateutil<3.0.0,>=2.1 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from botocore==1.34.145->awscli) (2.9.0.post0)
Requirement already satisfied: urllib3!=2.2.0,<3,>=1.25.4 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from botocore==1.34.145->awscli) (2.2.2)
Requirement already satisfied: pyasn1>=0.1.3 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from rsa<4.8,>=3.1.2->awscli) (0.6.0)
Requirement already satisfied: six>=1.5 in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (from python-dateutil<3.0.0,>=2.1->botocore==1.34.145->awscli) (1.16.0)

[notice] A new release of pip available: 22.3.1 -> 24.1.2
[notice] To update, run: python.exe -m pip install --upgrade pip

C:\Users\Student.MAT-42.000>aws configure
AWS Access Key ID [****************VEEN]:
AWS Secret Access Key [****************veEN]:
Default region name [us-east-1]:
Default output format [json]:
C:\Users\Student.MAT-42.000>pip install pycryptodome
Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: pycryptodome in c:\users\student.mat-42.000\appdata\roaming\python\python311\site-packages (3.20.0)

[notice] A new release of pip available: 22.3.1 -> 24.1.2
[notice] To update, run: python.exe -m pip install --upgrade pip
#open python

C:\Users\Student.MAT-42.000>python
Python 3.11.3 (tags/v3.11.3:f3909b8, Apr  4 2023, 23:49:59) [MSC v.1934 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from Crypto.Cipher import AES
>>> from Crypto.Random import get_random_bytes
>>> import base64
>>>
>>> def pad(data):
...     # PKCS7 padding
...     pad_len = 16 - (len(data) % 16)
...     return data + chr(pad_len) * pad_len
...
>>> def unpad(data):
...     # PKCS7 unpadding
...     pad_len = ord(data[-1])
...     return data[:-pad_len]
...
>>> def encrypt(data, key):
...     # Generate a random initialization vector (IV)
...     iv = get_random_bytes(16)
...     cipher = AES.new(key, AES.MODE_CBC, iv)
...     padded_data = pad(data)
...     encrypted_data = cipher.encrypt(padded_data.encode())
...     # Combine IV with encrypted data
...     return base64.b64encode(iv + encrypted_data).decode()
...
>>> def decrypt(encrypted_data, key):
...     # Decode from base64
...     encrypted_data = base64.b64decode(encrypted_data)
...     iv = encrypted_data[:16]
...     cipher = AES.new(key, AES.MODE_CBC, iv)
...     encrypted_data = encrypted_data[16:]
...     decrypted_data = cipher.decrypt(encrypted_data).decode()
...     return unpad(decrypted_data)
...
>>> # Example usage:
>>> key = get_random_bytes(16)  # AES key must be either 16, 24, or 32 bytes long
>>> data = "JEEVAHARISHPRAVEEN"
>>> encrypted = encrypt(data, key)
>>> print(f"Encrypted: {encrypted}")
Encrypted: E5Xs0rVMM9UhEjCWfY1WBNx6Se8VDejp7e7qMHlFeE70BA5bjfQNhZIbRJa+2RtY
>>>
>>> decrypted = decrypt(encrypted, key)
>>> print(f"Decrypted: {decrypted}")
Decrypted: JEEVAHARISHPRAVEEN
>>>
