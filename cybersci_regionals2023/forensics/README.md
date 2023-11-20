# XORacle Quest - Unveiling the Hidden Sauce

## Overview
We were given an APK and a hint that the admin had left some sort of admin token in it. They wanted the decrypted admin token.


## Solution
1. Decompile the given apk for the source code.

2. Search for strings related to admin token.

3. In QRCodeActivity.java, we see where the `ADMIN_TOKEN` is set. We can also find where sauce is retrieved from later.

```java
String value = intent.getStringExtra("key");
this.sauce = intent.getStringExtra("sauce");
this.ADMIN_TOKEN = getToken();
```

In the `getToken()` function, there's a simple XOR encryption of the sauce.

```java
public String getToken() {
        String str = this.sauce;
        if (str != null) {
            byte[] obfuscatedBytes = str.getBytes();
            for (int round = 2; round >= 0; round--) {
                for (int i = obfuscatedBytes.length - 1; i >= 0; i--) {
                    obfuscatedBytes[i] = (byte) (obfuscatedBytes[i] ^ ((byte) (i + round)));
                }
            }
            return new String(obfuscatedBytes);
        }
        throw new AssertionError();
    }
```

4. Let's look for sauce in the source code. It's retrieved from `public.xml`. The encrypted admin token:
```xml
<string name="sauce">@0a1X4k`~{n>{=!`Lg!`\"</string>
```

5. Decode the XOR'd admin token

```java
public String decodeToken(String obfuscatedToken) {
        byte[] obfuscatedBytes = obfuscatedToken.getBytes();
        for (int round = 0; round <= 2; round++) {
            for (int i = 0; i < obfuscatedBytes.length; i++) {
                obfuscatedBytes[i] = (byte) (obfuscatedBytes[i] ^ ((byte) (i + round)));
            }
        }
        return new String(obfuscatedBytes);
    }
```


## Flag
```C0d3_0bfusc4t10n_w4r5```

----
Special thanks to Arctic for teaching me Cryptography in second year 🥹, really came in handy here.