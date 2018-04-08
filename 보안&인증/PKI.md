## PKI(Public Key Infrastructure)

### Cryptographic Hash Function(암호화 해쉬함수)

- Message Digest(메시지 축약)
    + 아무리 긴 파일이라도 간단하게 축약
    + 대표적인 암호화 알고리즘: MD5(128bit), SHA-1(160bit)

- Symmetric Key Algorithm(대칭키 알고리즘)
    + 키를 한 개만 이용 하는 것
    + 인크립션 (Encryption) 과 디크립션 (Decryption) 시 한개의 같은 키를 이용

- Asymmetric Key Algorithm(비대칭키 알고리즘)
    + 두개의 키를 이용: Private Key(개인키), Public Key(공개키)
    + 대표적인 알고리즘: RSA
    + 공개키(Public Key)를 이용해서 인크립션(Encryption)을 한다면 다시 디크립션(Decryption)할려면 꼭 쌍이 이루어 지는 개인키(Private Key)를 이용, 공개키 '암호화'
    + 개인키(Private Key)를 가지고 인크립션(Encryption) 하는 경우, Encrypted Text 를 쌍이 되는 공개키(Public Key)로 풀어줘야 함, 개인이 보낸 내용을 증명할 때 많이 쓰임, 개인키 전자서명
