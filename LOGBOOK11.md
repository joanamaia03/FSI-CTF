# Trabalho realizado na Semana #11

## Task 1: Becoming a Certificate Authority (CA)
Copiamos o config e descomentamos a linha que continha o unique_subject.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image7.png)
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image8.png)

```
openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -keyout ca.key -out ca.crt
```
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image9.png)

```
openssl x509 -in ca.crt -text -noout
openssl rsa -in ca.key -text -noout
```
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image10.png)

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image11.png)

```
Enter pass phrase for ca.key:
RSA Private-Key: (4096 bit, 2 primes)
modulus:
    00:ad:2e:4e:6f:d4:b1:10:6c:fe:63:dd:6e:27:d5:
    df:c8:f4:11:09:5d:a9:03:13:04:07:ce:6a:94:95:
    2c:ff:a0:ef:1c:c8:ef:17:a4:d1:dc:37:b3:ce:97:
    15:f9:5a:b9:41:c3:c8:4f:37:00:9f:89:e9:71:ba:
    5f:b7:68:ec:fc:7c:cf:ac:e6:f8:66:4d:73:35:63:
    69:ff:96:33:b2:14:2e:b2:93:6c:a7:78:34:d7:17:
    0a:69:f6:02:66:f8:ff:15:b4:30:b8:e4:f2:ef:65:
    11:01:f2:85:fd:8c:6b:d3:cb:40:f7:0b:db:64:5d:
    b3:94:da:30:ca:2d:3c:5a:f5:37:8e:bb:43:8b:2a:
    b4:14:18:30:06:0e:ea:7d:ce:2b:6a:22:08:8c:e3:
    a7:9d:ff:60:89:cc:28:e6:33:dd:bb:38:54:94:1a:
    1c:51:cd:ad:e8:01:29:b3:f0:47:76:96:ac:30:bc:
    b3:88:76:4b:4d:2d:6b:43:80:1a:83:62:a9:5e:3b:
    75:26:6e:2b:d9:3e:b4:8c:b8:aa:8e:b9:19:75:20:
    76:71:5f:be:91:cb:4f:d3:99:a1:bc:33:1a:83:9c:
    6e:0a:1e:96:9c:64:10:19:1b:a5:36:4e:9e:07:0b:
    fa:28:d5:9d:15:b4:2d:6a:fe:11:00:f2:2c:eb:0a:
    9b:94:79:e5:46:85:09:64:10:38:99:0c:f4:c3:c7:
    5f:86:25:25:30:bc:4e:d3:06:34:0b:de:f9:d6:ba:
    bf:8f:25:be:96:74:08:68:61:9a:a9:0c:f1:6f:41:
    5c:bd:ec:4a:d8:94:13:cb:45:6c:77:6d:aa:45:71:
    e1:57:05:29:4a:73:a3:7a:a4:fe:6b:59:21:2f:17:
    a4:7f:fa:ac:c2:4b:f0:cf:49:46:a2:df:e1:db:f8:
    26:14:e8:1f:ea:50:72:ab:bd:05:93:0b:39:69:0f:
    68:19:94:ed:05:75:52:62:da:c7:5e:49:29:82:eb:
    b7:b7:e8:32:51:c7:3b:09:e6:78:51:f6:1f:81:11:
    91:e6:ba:94:8c:d6:fa:c5:7e:8f:63:b5:74:cd:f6:
    c4:ea:e2:81:d4:0b:69:aa:df:8c:dd:30:37:c9:b7:
    1b:a9:b2:db:ba:35:e6:80:1e:81:53:99:dc:42:93:
    f9:e1:2b:00:fa:81:db:39:fb:a1:ae:7d:59:ce:96:
    3d:aa:29:16:5f:7a:1c:67:c0:47:c2:5c:0b:19:db:
    a0:e0:55:ac:de:23:60:e6:08:ff:58:3e:cd:58:63:
    32:f7:8a:fd:48:39:8b:4f:47:79:3a:55:7e:0e:fb:
    c6:51:46:12:f5:96:4d:b5:df:26:e2:5e:b3:71:5d:
    90:da:0d
publicExponent: 65537 (0x10001)
privateExponent:
    50:67:db:8b:18:99:4d:23:0d:c9:98:19:78:ed:58:
    05:99:2b:ff:c9:38:9b:70:cc:c2:43:18:40:fc:31:
    f4:4d:e8:36:d9:24:09:3a:41:25:99:c7:25:f8:07:
    ff:ca:1b:91:69:31:2b:76:42:17:d0:94:4e:75:55:
    d3:76:27:f1:e2:91:19:99:f3:62:ac:3a:fd:62:b6:
    e8:2f:f8:b8:89:9e:54:d3:15:f3:7b:60:2d:2d:49:
    6c:81:08:04:7f:3f:0f:f8:a5:56:73:16:48:08:08:
    a9:7a:cc:b3:37:eb:28:5e:8a:3f:29:86:27:47:4a:
    05:a6:78:58:a6:40:0b:8b:26:cc:62:2d:ae:03:99:
    b0:6a:ba:81:55:93:91:ed:93:42:a7:a2:88:a7:7a:
    3f:65:3e:91:3b:f5:11:4c:ab:7a:2d:61:37:92:17:
    eb:f3:2e:f7:34:f3:03:d4:5f:99:b3:c3:26:ad:b6:
    3d:79:8e:e4:ba:5d:be:ed:4f:62:09:00:d1:fb:91:
    1c:d2:b2:11:1f:87:fc:7e:10:d2:4b:26:82:b7:1b:
    c6:ef:c9:2f:2f:d2:54:50:54:43:69:06:ba:6c:7a:
    ba:c0:10:f5:73:8f:f5:d8:5c:10:a6:d7:c0:35:d3:
    63:fa:2a:00:d5:b2:f0:a6:1d:86:ee:e9:e4:06:fc:
    cc:63:41:39:ab:7b:0e:ae:67:d2:d6:1b:51:49:54:
    f0:c0:c3:c2:7e:e8:c9:5e:01:46:e7:84:35:a6:20:
    9d:0f:94:a7:64:d5:dc:ab:97:17:fd:25:01:6c:38:
    cc:fa:0e:83:c9:1c:4d:cb:b3:61:24:1f:c1:14:78:
    26:c5:4a:e1:40:cf:5e:67:26:6f:86:28:da:4b:2f:
    f1:e1:18:88:8e:c5:2f:3e:b3:82:48:ca:45:13:80:
    c5:c7:f1:ac:ca:23:16:fa:a8:4f:f7:f8:5e:a7:c4:
    d8:7c:43:e6:c8:6f:e5:21:3b:d6:23:79:e5:2f:3b:
    62:e0:7d:a8:ee:ea:2c:df:94:3b:d1:45:8c:92:92:
    83:ea:0e:cb:33:a9:33:71:21:93:32:33:a5:24:79:
    b9:7a:dc:ca:a3:17:f1:18:bb:75:91:6d:9f:85:82:
    8d:3a:75:87:a7:23:7a:c2:af:1a:32:09:91:26:60:
    79:5c:45:7c:32:b3:20:14:b0:2b:9a:b0:2e:c3:52:
    44:b1:42:68:b7:d8:03:2e:96:3e:4d:1f:38:5a:23:
    de:05:d2:fe:66:1d:38:3a:3b:71:c9:37:ab:5b:2b:
    21:52:1e:b4:a7:6e:c4:39:a3:43:3d:90:38:bc:e5:
    b2:c1:7c:c6:a2:44:e3:e2:a3:d0:b0:ad:ee:e6:89:
    d1:81
prime1:
    00:dc:83:c1:dc:a8:2b:27:b0:c1:84:54:26:f2:76:
    cc:2c:66:ae:54:7d:92:86:d8:b8:f1:a5:62:85:70:
    74:bb:40:11:0c:fe:25:87:26:25:5b:9c:13:e1:30:
    10:07:29:4a:48:4c:95:08:db:98:1c:38:65:bf:29:
    f9:ca:9c:37:f3:ee:2b:d6:95:9a:2b:3d:0c:dd:22:
    4d:86:85:c8:99:a6:ca:71:22:8e:d2:d9:f6:cd:53:
    2a:53:ff:87:25:1a:6a:4f:35:a1:d1:d2:2c:24:a4:
    b5:ac:8e:cb:b4:87:c6:10:7f:11:45:23:b7:95:26:
    2f:bc:55:1d:a7:38:90:8b:3f:03:62:0c:83:b4:2b:
    d5:35:b0:51:bb:14:ea:8e:85:60:d7:05:ff:e7:11:
    fd:26:e5:98:11:85:7e:2b:c5:d4:f8:07:20:92:14:
    09:78:c8:22:a2:89:0a:b5:71:ff:e6:f8:60:3a:94:
    0f:1a:26:65:0a:6f:8c:63:96:5c:c8:8d:9e:7c:80:
    0a:8f:12:1a:c6:5e:a1:30:fd:b2:43:ad:f8:5a:10:
    a7:25:75:8a:04:a8:6e:02:c1:00:16:c4:56:6a:56:
    58:be:30:1e:86:f1:c6:37:cb:78:9b:4d:b2:71:2c:
    5a:ed:ca:c9:39:ee:99:0c:10:35:3b:07:48:cb:ac:
    8e:45
prime2:
    00:c9:0c:9a:75:86:0d:eb:bd:82:23:a6:4e:1c:81:
    1f:d3:59:e4:7b:71:78:fa:4d:a7:30:23:94:65:0b:
    3b:42:88:8e:f2:8e:45:21:29:9b:1d:03:ed:9f:4a:
    0c:67:23:41:b4:56:84:36:06:fc:ef:e9:07:9b:e3:
    97:44:b3:50:86:3b:52:51:95:26:48:81:f6:a5:b5:
    79:c1:91:68:15:b8:3f:f9:55:5f:3a:cb:67:97:9b:
    f3:27:77:01:2c:38:82:de:a8:4f:73:6b:27:3e:42:
    d5:35:6e:40:a6:2e:d1:8c:85:49:26:c0:a1:a1:e1:
    2b:dc:92:95:1b:d8:1b:3f:48:49:a7:02:6a:b3:ff:
    00:59:e4:c2:3d:58:84:ef:1f:35:c1:21:71:13:94:
    1e:97:a6:48:b2:b1:6c:89:67:44:f4:c1:7f:04:a3:
    50:f7:0c:be:22:f8:7b:a6:d4:dd:29:9e:e6:e4:92:
    e2:6a:3f:1a:20:3b:17:d6:b4:52:b9:b6:78:28:00:
    41:b6:8f:e9:9e:18:9d:24:f7:81:0a:6b:26:e1:11:
    c0:d4:89:45:b5:04:e0:26:ec:6e:aa:31:8e:14:89:
    97:fd:d5:7c:4c:5d:bc:8c:19:56:b4:00:51:a9:79:
    7d:66:ec:cd:c5:09:7b:0e:b9:7f:07:c0:7d:11:b3:
    5d:29
exponent1:
    00:c0:08:3d:9a:db:18:39:c8:43:bd:e9:4a:c1:7b:
    92:f2:57:b9:18:fb:01:cf:4c:8c:42:63:b4:18:60:
    86:47:4a:d3:8e:6d:04:61:5d:66:cb:10:70:7f:7a:
    4b:7a:f1:0a:2f:4c:01:bd:64:fe:62:14:fb:06:2e:
    97:c9:49:a1:b0:5b:88:f1:a5:f6:4c:11:2e:52:a4:
    bc:be:99:62:c7:eb:e7:ff:fe:08:42:b6:6d:a7:00:
    f5:ab:90:ab:30:34:80:bf:da:04:c1:a4:35:ac:f3:
    83:02:72:98:12:ee:ea:1d:13:8b:06:9a:c4:14:ae:
    dc:83:35:dc:4c:f3:85:6c:bd:c3:44:6f:81:82:35:
    69:c7:07:75:25:66:61:9d:1b:a9:e9:96:df:f3:6a:
    46:fa:c8:96:55:2b:db:64:63:33:c3:8a:f1:62:44:
    f0:ba:ae:0e:fb:5c:3c:67:26:8f:a3:a4:48:a8:ba:
    a7:2c:2e:a3:6f:23:15:2e:e4:92:88:54:4b:e0:3f:
    e0:f2:16:e2:1a:3d:ee:41:ab:ac:c2:23:8e:53:60:
    8d:2e:a1:dd:3f:91:2d:bc:58:36:ab:9c:ef:64:4b:
    2d:9c:f2:6a:a3:39:89:54:ad:6c:aa:52:4f:43:1f:
    4d:50:27:78:75:6a:c2:fd:2e:60:2c:b7:7b:3d:63:
    57:c1
exponent2:
    00:93:e1:ef:63:6e:dd:a2:7f:5c:d0:78:2d:90:8d:
    f2:28:f6:40:38:04:b9:65:f3:e4:7c:66:4f:6b:1b:
    9d:d5:4c:b9:48:f5:19:28:51:80:45:11:74:a1:ec:
    47:bf:3d:91:c0:e2:ba:91:3b:06:a6:39:94:5d:38:
    45:36:45:67:7f:b4:f6:d2:07:91:87:58:01:62:d6:
    5f:de:df:e3:dd:c6:0f:58:89:51:68:df:e1:2d:05:
    8b:0f:86:5b:98:79:60:da:02:97:9e:60:3d:17:70:
    f5:7f:3d:bf:d3:fd:30:29:da:88:7a:36:cb:2d:55:
    81:7b:d7:5e:52:82:dd:57:e9:06:34:10:75:08:3d:
    13:b7:0b:ab:4c:90:66:07:b5:bf:46:76:20:c4:b3:
    f8:e4:b7:6d:55:f3:67:d0:91:e3:88:dd:23:5e:f7:
    fa:40:1e:61:65:3b:bd:48:73:de:d2:14:8d:e5:a7:
    9d:5f:65:57:04:4a:33:38:bc:9e:f4:f7:a0:de:5b:
    81:fa:95:54:d3:f3:6a:f3:9c:12:90:e5:4c:4d:d5:
    4f:2f:86:61:7d:cb:3e:4d:a3:2f:ab:84:93:eb:cb:
    61:bf:56:5e:fd:95:1d:71:37:da:2c:c0:e7:50:6f:
    8a:ac:40:97:02:cd:fc:74:52:41:7c:24:3c:5a:de:
    c2:31
coefficient:
    27:f2:42:78:2f:b6:f8:8b:ed:31:17:c0:94:2b:10:
    ad:c3:8a:e9:e0:bb:7a:85:e7:84:ab:40:4e:4c:6e:
    41:7e:79:8d:64:85:36:8b:53:7b:c5:bd:48:6a:95:
    ec:6e:fd:7f:f8:95:33:6a:2b:d5:46:c7:d9:3f:11:
    14:3e:71:7d:4c:97:2b:5f:cc:af:15:4b:62:f2:8b:
    ce:00:49:bf:c3:d4:54:02:6a:14:a0:08:e6:d8:22:
    e7:41:85:b9:20:53:f5:9d:5f:0c:19:f7:ef:bf:c5:
    ba:97:ec:d8:eb:52:f1:a1:51:26:b6:06:8f:50:9c:
    e1:15:b0:f8:72:92:b9:95:10:92:fa:93:e2:dc:5b:
    76:29:a4:d0:11:4c:95:f3:23:23:41:fa:36:cb:38:
    2b:8b:07:7d:96:4a:19:bc:92:af:f3:c0:55:4b:3c:
    e4:3b:e9:cb:0a:d0:1f:05:9c:de:51:9b:ee:e3:81:
    cd:6c:5a:d0:67:ad:a7:12:18:1e:ce:99:ab:4c:e7:
    e7:22:ee:5d:95:96:7e:96:a0:fe:25:16:43:da:d2:
    17:6e:33:57:54:84:f4:f2:c8:42:90:97:56:60:48:
    62:ea:3e:78:22:21:a1:bd:3c:ca:1f:9a:22:a5:8c:
    84:63:01:6e:56:57:78:17:47:42:27:1a:2c:44:29:
    1c
```

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image12.png)

```
    Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            0b:be:e4:8a:03:9d:9b:09:16:af:7f:d1:21:10:ac:2f:e2:5c:13:70
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = pt, ST = porto, L = porto, O = feup, OU = leic, CN = juana, emailAddress = juanita@gmail.com
        Validity
            Not Before: Dec 10 16:29:38 2023 GMT
            Not After : Dec  7 16:29:38 2033 GMT
        Subject: C = pt, ST = porto, L = porto, O = feup, OU = leic, CN = juana, emailAddress = juanita@gmail.com
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                RSA Public-Key: (4096 bit)
                Modulus:
                    00:ad:2e:4e:6f:d4:b1:10:6c:fe:63:dd:6e:27:d5:
                    df:c8:f4:11:09:5d:a9:03:13:04:07:ce:6a:94:95:
                    2c:ff:a0:ef:1c:c8:ef:17:a4:d1:dc:37:b3:ce:97:
                    15:f9:5a:b9:41:c3:c8:4f:37:00:9f:89:e9:71:ba:
                    5f:b7:68:ec:fc:7c:cf:ac:e6:f8:66:4d:73:35:63:
                    69:ff:96:33:b2:14:2e:b2:93:6c:a7:78:34:d7:17:
                    0a:69:f6:02:66:f8:ff:15:b4:30:b8:e4:f2:ef:65:
                    11:01:f2:85:fd:8c:6b:d3:cb:40:f7:0b:db:64:5d:
                    b3:94:da:30:ca:2d:3c:5a:f5:37:8e:bb:43:8b:2a:
                    b4:14:18:30:06:0e:ea:7d:ce:2b:6a:22:08:8c:e3:
                    a7:9d:ff:60:89:cc:28:e6:33:dd:bb:38:54:94:1a:
                    1c:51:cd:ad:e8:01:29:b3:f0:47:76:96:ac:30:bc:
                    b3:88:76:4b:4d:2d:6b:43:80:1a:83:62:a9:5e:3b:
                    75:26:6e:2b:d9:3e:b4:8c:b8:aa:8e:b9:19:75:20:
                    76:71:5f:be:91:cb:4f:d3:99:a1:bc:33:1a:83:9c:
                    6e:0a:1e:96:9c:64:10:19:1b:a5:36:4e:9e:07:0b:
                    fa:28:d5:9d:15:b4:2d:6a:fe:11:00:f2:2c:eb:0a:
                    9b:94:79:e5:46:85:09:64:10:38:99:0c:f4:c3:c7:
                    5f:86:25:25:30:bc:4e:d3:06:34:0b:de:f9:d6:ba:
                    bf:8f:25:be:96:74:08:68:61:9a:a9:0c:f1:6f:41:
                    5c:bd:ec:4a:d8:94:13:cb:45:6c:77:6d:aa:45:71:
                    e1:57:05:29:4a:73:a3:7a:a4:fe:6b:59:21:2f:17:
                    a4:7f:fa:ac:c2:4b:f0:cf:49:46:a2:df:e1:db:f8:
                    26:14:e8:1f:ea:50:72:ab:bd:05:93:0b:39:69:0f:
                    68:19:94:ed:05:75:52:62:da:c7:5e:49:29:82:eb:
                    b7:b7:e8:32:51:c7:3b:09:e6:78:51:f6:1f:81:11:
                    91:e6:ba:94:8c:d6:fa:c5:7e:8f:63:b5:74:cd:f6:
                    c4:ea:e2:81:d4:0b:69:aa:df:8c:dd:30:37:c9:b7:
                    1b:a9:b2:db:ba:35:e6:80:1e:81:53:99:dc:42:93:
                    f9:e1:2b:00:fa:81:db:39:fb:a1:ae:7d:59:ce:96:
                    3d:aa:29:16:5f:7a:1c:67:c0:47:c2:5c:0b:19:db:
                    a0:e0:55:ac:de:23:60:e6:08:ff:58:3e:cd:58:63:
                    32:f7:8a:fd:48:39:8b:4f:47:79:3a:55:7e:0e:fb:
                    c6:51:46:12:f5:96:4d:b5:df:26:e2:5e:b3:71:5d:
                    90:da:0d
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Subject Key Identifier: 
                89:17:66:CC:20:DB:60:DD:60:BE:B5:18:05:29:A7:03:72:61:5D:12
            X509v3 Authority Key Identifier: 
                keyid:89:17:66:CC:20:DB:60:DD:60:BE:B5:18:05:29:A7:03:72:61:5D:12

            X509v3 Basic Constraints: critical
                CA:TRUE
    Signature Algorithm: sha256WithRSAEncryption
         9e:9d:e8:a4:a6:b9:28:f3:f1:c8:9a:b5:e8:88:24:1c:06:12:
         b6:15:0b:9f:34:c7:8a:70:ec:02:58:dc:dd:e0:e9:52:10:20:
         e7:f6:0e:17:bd:4b:9b:c9:15:84:b1:48:93:8d:3f:97:7e:f2:
         72:df:07:1f:97:c9:c0:2d:c0:c9:a3:4e:1c:ca:87:b4:ab:76:
         d7:8f:bb:91:04:6c:a4:3e:46:4d:75:15:9d:c0:3c:43:69:ce:
         64:9a:d4:0f:1e:fb:c4:d8:7a:66:c2:4a:c9:a6:73:b2:b1:a4:
         9d:58:c0:36:cc:55:e7:83:9f:8e:df:eb:34:5c:35:50:93:46:
         d6:f8:9c:84:bc:fe:25:a5:02:5a:47:94:00:d3:fa:9a:f7:ed:
         3c:30:a0:be:bf:32:b3:4a:97:11:8b:65:42:45:4a:09:fc:1d:
         72:14:da:07:7f:f4:1e:90:5a:dc:98:c5:07:3b:1d:6e:2c:f6:
         f8:5c:8e:4b:3d:a1:37:2d:65:c1:4d:df:6f:d5:b2:9a:33:4a:
         89:2e:4b:23:a7:5c:44:ee:ce:b3:db:6b:87:c5:75:a6:d6:cf:
         d4:f3:6e:fa:4d:9d:64:97:22:79:02:e3:38:73:b7:f0:1d:cc:
         d3:54:5b:2b:fb:50:ac:7a:5e:ec:63:67:e0:91:87:bb:50:8b:
         97:f0:c2:f4:e3:80:b8:91:5f:63:3c:16:aa:0b:73:1f:c2:08:
         e6:ea:95:2e:54:e5:8b:18:69:d9:0e:83:d2:77:86:97:fe:d2:
         94:ac:4f:d3:58:75:90:31:1f:7d:35:3d:4c:a4:c9:97:03:35:
         01:6c:6f:13:ba:23:fe:0c:a1:e9:8f:57:7c:39:4e:7b:a2:b9:
         9f:1d:4f:f3:8a:11:24:fd:6d:6f:50:10:54:84:77:5a:0f:c9:
         fd:5b:2a:e3:c5:cc:ac:2f:d1:b6:53:45:5f:f8:01:52:8e:d7:
         63:3e:2d:eb:90:b8:10:a8:86:e5:7d:f6:57:37:bc:64:95:22:
         a0:28:3a:28:5d:19:c8:2a:45:41:f0:48:04:2c:2f:70:26:ae:
         14:be:8d:7d:d0:44:5e:86:c8:53:aa:8d:d9:04:5d:3d:5f:76:
         d4:f7:2a:b7:bb:7c:8f:18:70:1a:ce:dc:08:57:c6:ac:9e:39:
         59:a1:93:8e:f2:c2:71:d8:bf:3f:b6:d3:cb:10:09:0a:a0:8a:
         6a:7d:1c:5d:df:02:97:13:b0:4a:bf:26:fe:16:72:f2:82:c3:
         42:84:6e:1c:41:1c:d7:4d:19:06:47:0a:bb:1f:84:77:9a:81:
         49:71:ca:8a:55:77:c5:dd:20:55:99:10:46:84:fe:15:45:ae:
         ca:80:cb:71:cc:40:39:e1
```

Que parte do certificado indica que é um certificado CA?
- No campo "Basic Constraints", caso CA:TRUE, então é um certificado CA.

Que parte do certificado indica que este é self-signed?
- No campo "Issuer" caso este seja o mesmo que o do campo "Subject", então é um certificado self-signed.

No algoritmo RSA, temos um expoente público e, um expoente privado d, um modulus n, e dois números secretos p e q, tal que n = pq. Por favor indica os valores destes elementos no certificado e o ficheiro key.
- Procurar pelo expoente público e, o expoente privado d, e o modulus n nos detalhes da chave RSA.

## Task 2:  Generating a Certificate Request for Your Web Server
O comando apresentado abaixo gera a CSR para o specified common name (www.fsi2023.com) e inclui nomes alternativos (www.fsi2023A.com and www.fsi2023B.com), usando a extensão Subject Alternative Name.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image13.png)

## Task 3: Generating a Certificate for your server
O comando openssl ca é usado para assinar o CSR e gerar o certificado X.509.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image14.png)
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image15.png)

## Task 4: Deploying Certificate in an Apache-Based HTTPS Website

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image16.png)
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook%2011/image17.png)
