**1.javax.crypto.IllegalBlockSizeException: last block incomplete in decryption**

**问题描述：**
AES解密的时候报错 javax.crypto.IllegalBlockSizeException: last block incomplete in decryption。

**报错原因：**
使用AES加密后还需使用Base64编码方式再进行一次加密，所以解密的时候需要先用Base64解密，再用AES的方法解密。

**解决方法：**
使用Aes解密之前先使用Base64解密一次。


```kotlin
package com.wkz.util.encryption

import android.util.Base64
import java.security.NoSuchAlgorithmException
import javax.crypto.Cipher
import javax.crypto.KeyGenerator
import javax.crypto.SecretKey
import javax.crypto.spec.IvParameterSpec
import javax.crypto.spec.SecretKeySpec

/**
 * AES对称加密:
 * Advanced Encryption Standard，高级数据加密标准，AES算法可以有效抵制针对DES的攻击算法，对称加密算法
 */
class AESUtil private constructor() {
    companion object {

        /**
         * 偏移量
         */
        private const val offset = 16

        /**
         * 加密器类型:加密算法为AES,加密模式为CBC,补码方式为PKCS5Padding
         */
        private const val transformation = "AES/CBC/PKCS5Padding"

        /**
         * 算法类型：用于指定生成AES的密钥
         */
        private const val algorithm = "AES"

        /**
         * 生成密钥
         */
        @Throws(NoSuchAlgorithmException::class)
        fun initKey(): ByteArray {
            val keyGen = KeyGenerator.getInstance(algorithm)
            keyGen.init(256) //192 256
            val secretKey = keyGen.generateKey()
            return secretKey.encoded
        }

        /**
         * AES 加密
         */
        @Throws(Exception::class)
        fun encrypt(data: ByteArray, key: ByteArray? = null): ByteArray {
            // 构造密钥
            val secretKey: SecretKey = SecretKeySpec(key ?: initKey(), algorithm)
            //  创建初始向量iv用于指定密钥偏移量(可自行指定但必须为128位)，因为AES是分组加密，
            //  下一组的iv就用上一组加密的密文来充当
            val ivParameterSpec = IvParameterSpec(key ?: initKey(), 0, offset)
            // 创建AES加密器
            val cipher = Cipher.getInstance(transformation)
            // 使用加密器的加密模式
            cipher.init(Cipher.ENCRYPT_MODE, secretKey, ivParameterSpec)
            // 加密
            val result = cipher.doFinal(data)
            // 使用BASE64对加密后的二进制数组进行编码
            return Base64.encode(result, Base64.DEFAULT)
        }

        /**
         * AES 加密
         */
        @Throws(Exception::class)
        fun encrypt(data: String, key: ByteArray? = null): String {
            return encrypt(data.toByteArray(), key).toString()
        }

        /**
         * AES 解密
         */
        @Throws(Exception::class)
        fun decrypt(data: ByteArray, key: ByteArray? = null): ByteArray {
            // 构造密钥
            val secretKey: SecretKey = SecretKeySpec(key ?: initKey(), algorithm)
            //  创建初始向量iv用于指定密钥偏移量(可自行指定但必须为128位)，因为AES是分组加密，
            //  下一组的iv就用上一组加密的密文来充当
            val ivParameterSpec = IvParameterSpec(key ?: initKey(), 0, offset)
            // 创建AES加密器
            val cipher = Cipher.getInstance(transformation)
            // 解密时使用加密器的解密模式
            cipher.init(Cipher.DECRYPT_MODE, secretKey, ivParameterSpec)
            return cipher.doFinal(Base64.encode(data, Base64.DEFAULT))
        }

        /**
         * AES 解密
         */
        @Throws(Exception::class)
        fun decrypt(data: String, key: ByteArray? = null): String {
            return decrypt(data.toByteArray(), key).toString()
        }
    }

    init {
        throw UnsupportedOperationException("cannot be instantiated")
    }
}
```

**2.javax.crypto.IllegalBlockSizeException: error:1e00007b:Cipher functions:OPENSSL_internal:WRONG_FINAL_BLOCK_LENGTH**

**问题描述：**
AES加密没有问题，但是解密的时候一直报错 javax.crypto.IllegalBlockSizeException: error:1e00007b:Cipher functions:OPENSSL_internal:WRONG_FINAL_BLOCK_LENGTH。

**报错原因：**

- **toString()错误使用**

	无论加密字符串内容和长度如何改变，加密的结果总是"[B@xxxxxx"的形式，这肯定是有问题的，AES作为高强度的加密算法加密内容改变后加密结果开头还是一样这是不可能的，对称加密加密结果长度不随加密内容长短变化这也是不可能的。
	
- **ByteArray转String再转ByteArray内容发生改变引起错误**

	new String()默认使用UTF-8编码getBytes()默认使用ISO8859-1编码引发了问题，指定new String()和getBytes()统一使用ISO8859-1即可解决问题。
	
**解决方法：**
```kotlin
package com.wkz.util.encryption

import android.util.Base64
import java.nio.charset.Charset
import java.security.NoSuchAlgorithmException
import javax.crypto.Cipher
import javax.crypto.KeyGenerator
import javax.crypto.SecretKey
import javax.crypto.spec.IvParameterSpec
import javax.crypto.spec.SecretKeySpec

/**
 * AES对称加密:
 * Advanced Encryption Standard，高级数据加密标准，AES算法可以有效抵制针对DES的攻击算法，对称加密算法
 */
class AESUtil private constructor() {
    companion object {

        /**
         * 偏移量
         */
        private const val offset = 16

        /**
         * 加密器类型:加密算法为AES,加密模式为CBC,补码方式为PKCS5Padding
         */
        private const val transformation = "AES/CBC/PKCS5Padding"

        /**
         * 算法类型：用于指定生成AES的密钥
         */
        private const val algorithm = "AES"

        /**
         * 生成密钥
         */
        @Throws(NoSuchAlgorithmException::class)
        fun initKey(): ByteArray {
            val keyGen = KeyGenerator.getInstance(algorithm)
            keyGen.init(256) //192 256
            val secretKey = keyGen.generateKey()
            return secretKey.encoded
        }

        /**
         * AES 加密
         */
        @Throws(Exception::class)
        fun encrypt(data: ByteArray, key: ByteArray? = null): ByteArray {
            // 构造密钥
            val secretKey: SecretKey = SecretKeySpec(key ?: initKey(), algorithm)
            //  创建初始向量iv用于指定密钥偏移量(可自行指定但必须为128位)，因为AES是分组加密，
            //  下一组的iv就用上一组加密的密文来充当
            val ivParameterSpec = IvParameterSpec(key ?: initKey(), 0, offset)
            // 创建AES加密器
            val cipher = Cipher.getInstance(transformation)
            // 使用加密器的加密模式
            cipher.init(Cipher.ENCRYPT_MODE, secretKey, ivParameterSpec)
            // 加密
            val result = cipher.doFinal(data)
            // 使用BASE64对加密后的二进制数组进行编码
            return Base64.encode(result, Base64.DEFAULT)
        }

        /**
         * AES 加密
         */
        @Throws(Exception::class)
        fun encrypt(data: String, key: ByteArray? = null): String {
            // 不可以用ByteArray.toString().否则会报异常
            // javax.crypto.IllegalBlockSizeException: error:1e00007b:Cipher functions:OPENSSL_internal:WRONG_FINAL_BLOCK_LENGTH
            return String(encrypt(data.toByteArray(Charsets.ISO_8859_1), key), Charsets.ISO_8859_1)
        }

        /**
         * AES 解密
         */
        @Throws(Exception::class)
        fun decrypt(data: ByteArray, key: ByteArray? = null): ByteArray {
            // 构造密钥
            val secretKey: SecretKey = SecretKeySpec(key ?: initKey(), algorithm)
            //  创建初始向量iv用于指定密钥偏移量(可自行指定但必须为128位)，因为AES是分组加密，
            //  下一组的iv就用上一组加密的密文来充当
            val ivParameterSpec = IvParameterSpec(key ?: initKey(), 0, offset)
            // 创建AES加密器
            val cipher = Cipher.getInstance(transformation)
            // 解密时使用加密器的解密模式
            cipher.init(Cipher.DECRYPT_MODE, secretKey, ivParameterSpec)
            return cipher.doFinal(Base64.encode(data, Base64.DEFAULT))
        }

        /**
         * AES 解密
         */
        @Throws(Exception::class)
        fun decrypt(data: String, key: ByteArray? = null): String {
            // 不可以用ByteArray.toString().否则会报异常
            // javax.crypto.IllegalBlockSizeException: error:1e00007b:Cipher functions:OPENSSL_internal:WRONG_FINAL_BLOCK_LENGTH
            return String(decrypt(data.toByteArray(Charsets.ISO_8859_1), key), Charsets.ISO_8859_1)
        }
    }

    init {
        throw UnsupportedOperationException("cannot be instantiated")
    }
}
```