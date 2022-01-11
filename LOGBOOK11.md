# SEED Labs

## Public-Key Infrastructure (PKI) Lab

###  Task 1: Becoming a Certificate Authority (CA)

- What part of the certificate indicates this is a CA’s certificate?

- If the CA flag is true then it is a CA, otherwise then it is not a CA.

![Task 1](images/ca.png "Task 1: CA’s certificates")

- What part of the certificate indicates this is a self-signed certificate?

- We observed that boths the Subject key and the Authority identifier are the same, therefore it is a self-signed certificate.

![Task 1](images/ca.png "Task 1: Subject key and the Authority identifiers")

- In the RSA algorithm, we have a public exponent e, a private exponent d, a modulus n, and two secret
numbers p and q, such that n = pq. Please identify the values for these elements in your certificate
and key files.

- **modulus (n)**:
    00:b0:ad:7e:24:7d:75:43:1e:6a:9d:41:a9:de:54:
    08:6b:ea:d8:0e:25:70:14:6a:d7:d1:ff:8c:f8:d0:
    ad:e1:d2:56:08:aa:b2:2a:78:e9:43:a1:f6:4d:18:
    56:b3:06:0e:a4:28:0f:3a:10:c3:c8:38:f9:ae:9e:
    58:dc:fc:0a:23:8c:21:8a:fb:8a:da:9c:b3:d7:1e:
    32:96:1a:4b:a0:55:55:3d:2d:39:2d:df:28:05:04:
    a6:b2:79:f4:3e:3c:39:8e:f3:16:3c:09:96:ca:4e:
    7d:df:91:6e:c4:6a:48:db:2e:5f:02:92:69:5e:75:
    72:5b:66:ea:95:2f:e0:b5:25:ee:8c:9b:ef:a8:d7:
    a4:bf:52:be:c0:c8:00:e6:87:17:fa:66:e6:17:e8:
    53:70:76:bc:31:9f:d3:d4:01:7a:b5:8f:01:ef:c8:
    13:ec:c6:ce:39:df:12:f7:d7:e5:85:e1:6f:71:a8:
    74:7b:bc:04:9d:b4:86:ae:33:53:ba:8f:56:b5:4e:
    06:5b:43:a9:10:26:d2:69:cd:5f:32:8a:f4:2a:21:
    7c:88:b0:6e:a9:9e:be:e4:9c:a4:ee:4a:88:4d:d4:
    87:6c:f8:e4:79:b6:71:66:77:97:91:1b:8f:9f:ec:
    e1:2a:e2:a0:5e:14:a7:07:7a:e0:37:4e:97:11:72:
    2d:81:32:5a:dc:6b:03:1e:8d:bc:06:c4:2d:40:43:
    2f:3e:07:d2:bc:33:1f:06:11:86:f9:4e:df:96:a8:
    27:ba:9c:e9:cc:76:b5:e6:fb:37:b5:c3:99:fd:3a:
    64:68:52:4a:1e:41:18:bb:21:20:15:1a:6c:27:2b:
    f2:45:4a:5b:ac:05:16:1d:3d:2f:09:b5:42:95:09:
    a7:6a:a8:52:17:00:25:0d:cf:82:e8:ac:7d:bc:55:
    44:ce:40:66:63:c3:e4:1d:1c:30:ed:5b:86:7e:81:
    0b:d0:84:8a:06:c0:ed:70:e5:e2:ce:37:53:2a:68:
    c8:4f:44:86:43:ed:d6:b9:fd:93:e4:93:38:d9:48:
    55:4b:00:3b:33:09:15:c1:c4:d5:d3:91:e6:8a:e9:
    4c:3a:e4:87:48:05:4a:dc:6c:fc:92:58:75:a5:f4:
    68:f1:55:56:21:cf:21:13:0a:4c:20:e1:98:8c:9a:
    46:86:02:4d:f5:f9:0e:cf:c0:c2:72:f8:cc:95:45:
    88:5c:52:78:66:dd:10:32:ef:3c:cc:62:69:71:d6:
    b8:f2:a4:34:4b:31:3b:be:d8:bb:6b:67:6b:f0:7e:
    d3:dd:4c:62:3f:9e:a2:23:ad:0c:e9:0f:f8:24:e2:
    cb:d8:63:d7:5f:61:5d:b6:6f:a8:7d:d9:ec:c7:0d:
    40:6e:9d
- **publicExponent (e):** 65537 (0x10001)
- **privateExponent (d):**
    00:9b:94:7b:83:48:93:2d:42:a8:a1:c8:43:fc:cb:
    45:0b:3b:27:7c:f5:8c:c7:fd:fa:05:2b:a3:89:2b:
    c2:23:1c:a4:b4:47:14:53:80:5b:f1:39:bb:79:d2:
    57:ee:98:03:e6:9c:7c:24:26:c5:31:18:b3:0e:08:
    d4:b9:ec:9c:45:07:4e:36:64:21:b7:36:cc:cb:3f:
    05:4e:d6:e3:07:d2:7d:18:3d:2d:9f:ee:66:00:5d:
    43:29:e1:68:aa:31:40:82:58:1f:99:48:dc:67:54:
    4d:55:c5:6c:a4:3b:ef:e2:4a:e8:51:8c:7a:8b:3a:
    a3:34:47:e1:84:f4:3f:4d:65:94:b6:6f:4e:d1:00:
    ec:4b:aa:62:dd:c2:81:c0:7e:f0:27:89:db:4e:ec:
    40:25:c5:f9:1d:3d:e0:3c:4d:fd:2f:ca:39:eb:5b:
    e5:e7:d8:7d:9b:ca:8b:9a:82:9c:d4:93:5b:1e:dc:
    37:8f:0a:57:8a:44:81:60:ff:43:d9:02:06:59:eb:
    d6:7f:21:8a:cb:f5:53:ce:e5:91:d2:21:38:b7:ac:
    fb:4c:27:09:9c:06:75:95:3d:37:a3:bb:30:62:51:
    27:dc:57:24:62:e5:bc:e0:7d:a9:93:97:90:97:44:
    f2:57:60:6f:d5:c9:1b:f8:e3:44:74:8f:99:4a:3c:
    a0:42:30:b2:20:3b:f5:41:ed:a1:40:76:c4:8a:91:
    63:af:ae:48:18:67:78:5c:24:c8:37:63:c8:56:c3:
    74:27:d1:1b:7f:75:32:12:cf:14:ca:b9:5b:4c:52:
    42:cb:33:37:86:cd:ef:5d:3b:54:8a:1f:62:5a:bf:
    7e:66:85:06:bb:cd:10:e6:05:3b:85:40:86:6a:3e:
    73:21:b5:44:1e:54:06:7a:ae:6d:97:1d:90:c2:6e:
    fb:0e:f3:b8:ef:3f:f7:6a:e5:71:17:1b:71:39:14:
    f4:ad:48:ca:5d:02:d2:1f:fc:22:75:b5:15:31:de:
    ec:26:81:74:f1:58:20:78:dd:b4:86:b9:11:45:b4:
    55:6b:0d:5b:a4:92:35:2e:bb:36:54:1f:30:18:33:
    e9:53:20:d5:48:03:4f:a8:b0:ca:cd:84:c1:ed:30:
    52:19:66:7f:ad:9c:72:5d:37:de:c1:f5:c4:47:a2:
    d5:70:5c:82:97:d4:e3:2e:9b:d9:0d:a6:b8:35:0b:
    c6:38:74:13:27:97:86:4a:f8:e2:9f:1c:d6:ff:61:
    13:70:e7:04:a2:4d:cd:ce:2c:71:cb:ad:e8:ca:15:
    1f:a0:77:8f:22:66:e2:d6:4f:6f:c2:49:7f:f9:6f:
    b1:84:e8:44:ae:11:f7:76:5b:f3:08:e5:bd:54:87:
    0e:8c:81
- **p:**
    00:e2:b0:d7:ff:e6:ce:75:f1:e4:af:04:d6:db:29:
    f7:f2:d6:ff:d9:40:6e:ac:34:28:82:a1:26:10:e3:
    81:02:27:ca:ae:d9:1a:87:2d:28:cc:9d:83:bd:91:
    18:7d:20:88:85:04:65:6b:75:5a:55:0d:c0:f0:79:
    3d:f6:db:d0:10:7d:f7:58:56:23:08:68:53:f4:82:
    e0:dd:f5:c2:71:fd:a8:45:0b:0d:84:8e:b1:4e:fe:
    18:5b:87:e0:b2:8e:97:66:85:5d:39:53:c4:5b:c4:
    2d:2a:95:b2:e7:8e:b7:a0:5b:18:36:85:8d:fb:66:
    fe:98:90:37:d7:52:cf:c8:5b:78:2c:cf:8b:bc:26:
    6a:a1:38:45:6c:d7:49:8e:7f:9b:87:dc:70:5f:fd:
    48:87:9f:8e:02:03:cf:d9:64:13:a9:ef:97:7f:07:
    40:77:5d:b8:91:e3:fe:31:71:c2:2a:c4:2e:fb:2e:
    f0:e7:d6:50:6d:0e:3a:8c:32:f8:bb:4b:06:48:97:
    ff:d4:29:29:f1:23:2a:d0:f6:30:68:fa:27:c7:b9:
    5f:f0:34:39:16:7c:7b:8e:a4:b0:07:fb:54:74:7b:
    42:f1:c2:ee:ca:0c:c3:42:6b:31:03:f0:9b:39:77:
    5b:00:27:b5:8a:42:01:c2:1e:cc:e5:3e:47:7b:f1:
    61:fd
- **q:**
    00:c7:85:48:ae:99:bf:48:99:f4:56:f0:0f:a2:0a:
    7e:97:4b:10:74:00:9d:ce:16:c1:db:94:7a:ff:98:
    3e:7f:03:ac:67:85:76:f6:c9:5d:b3:1c:cb:c1:f7:
    9c:f9:0c:d0:47:10:6e:33:9a:5f:56:af:c4:32:d5:
    de:0f:c3:1f:17:f7:ad:d9:60:c9:c5:4c:dd:91:7b:
    d1:77:e5:eb:97:ac:97:14:d5:fc:e1:a4:a2:a6:27:
    10:ac:f4:89:4c:f3:16:00:48:31:2c:07:f4:32:89:
    0d:9d:9a:77:4d:ed:51:03:7a:47:9e:2e:29:b8:0a:
    65:72:5f:50:fc:69:2e:04:c6:34:c2:0a:0b:06:32:
    42:63:3f:c3:29:f5:6c:87:e1:b0:dc:a3:19:b4:f2:
    46:b8:3a:c6:b1:41:3c:f3:d2:46:84:30:9f:11:50:
    bc:f6:0b:2a:62:ee:36:72:ad:3b:26:36:be:44:0c:
    a9:0f:8a:bd:df:07:64:e8:3a:a3:86:b1:cf:0f:69:
    c9:db:ee:4c:21:17:33:9a:41:a8:a8:b2:4d:28:b1:
    1c:6c:1f:81:a9:30:0c:cf:a1:af:91:f8:b6:34:26:
    ba:40:6f:3f:a0:be:9b:7f:3c:73:fd:85:dd:0c:84:
    51:c4:8a:97:55:d4:9e:7c:da:26:73:4b:5e:3f:75:
    11:21

###  Task 2: Generating a Certificate Request for Your Web Server



