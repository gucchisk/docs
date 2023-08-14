# デジタル署名

## ライブラリ別IF

### Tink

#### sign
```java
KeysetHandle handle = CleartextKeysetHandle.read(JsonKeySetReader.withInputStream(inputStream));
PublicKeySign signer = handle.getPrimitive(PublicKeySign.class);
byte[] signature = signer.sign(message);
```

#### verify
```java
PublicKeyVerify verifier = handle.getPrimitive(PublicKeyVerify.class);
try {
  verifier.verify(signature, message);
} catch (GeneralSecurityException e) {
  // verification failure
}
```

### Java(util)

#### sign
```java
PrivateKey privateKey = ...
Signature signature = signature.getInstance(<algorithm>, <provider>);
signature.initSign(privateKey, SecureRandom)
signature.update(message);
byte[] signBytes = signature.sign();

```

#### verify
```java
PublicKey publicKey = ...
// Certificate certificate = ...
Signature signature = signature.getInstance(<algorithm>, <provider>);
signature.initVerify(publicKey)
// signature.initVerify(certificate)
signature.update(message);
boolean verified = signature.verify(signBytes);
```
