# HMAC 부호화 알고리즘

<img src="https://github.com/AI-Expo-2023/Chromatica-Client-V1/assets/100929676/d9ccde0d-b70b-4e66-8fe8-6323b5b3a901" width="400">

<aside>
❓ Hash-based message authentication code(HMAC)는 해시 함수와 비밀 키를 사용하는 암호화 인증 기술입니다.

</aside>

# HMAC란??

HMAC이란 REST API가 요청을 받았을 때, 이 요청이 신뢰할 수 있는 호출인지 확인하는 방법 중 하나입니다. 사용자의 ID와 암호 같이 민감한 정보를 직접 받을 필요 없이 사전에 공유한 secret key와 전송할 message를 입력받아서 Hash 기반의 MAC를 생성해서 전송하며 서버는 secret key와 message를 기반으로 MAC를 검증해서 secret key를 소유한 클라이언트가 보낸 메시지가 맞는지 인증할 수 있습니다.

### HMAC 키는 두가지 부분으로 구성합니다.

1. **Cryptographic keys:** 암호화 알고리즘은 데이터를 변경시키며, 수신자는 데이터를 다시 읽기 위해 특정 코드(key)가 필요합니다. HMAC은 공유된 비밀 키 세트에 의존합니다.
2. **Hash function**: 해시 알고리즘은 메시지를 한 번 더 변경시키거나 요약합니다. HMAC은 [SHA-1](https://sisiblog.tistory.com/317), [MD5](https://sisiblog.tistory.com/312), RIPEMD-128/60과 같은 [일반 암호화 해시 함수](https://www.rfc-editor.org/rfc/rfc2104)를 사용합니다.

이때 반드시 다음 사항을 만족해야합니다.

1. **Secret Keys**: 받은 메시지를 디코드할 방법이 있어야 합니다. 비밀 키가 이 일을 담당하며, 비밀 키는 비밀로 유지하고 숨겨야 합니다.
2. **Algorithm**: 모든 메시지에 적용할 하나의 해시 함수를 선택해야 합니다.

예시를 들어보자면 아래와 같이 요구를 했을 때에 결과를 확인할 수 있습니다.

- **Potential message**: 코인 100개 살래요
- **Secret key**: 666
- **Algorithm**: MD5

위 결과는 다음과 같습니다. : "d687d616768b50e2448300b9ada5dd0e”

이처럼 간단해 보이지만 엄청난 수학 계층이 깔려있다고 합니다.

그리고 개인 또는 웹 개발자로서 HMAC을 사용하려면 세 가지 중요 사항을 지켜야 합니다.

1. 수신자와 해당 항목에 대한 합의가 필요하므로 모두 동일한 도구를 사용해야 한다는 것 입니다. (같은 조건이어야한다.)
2. 공유된 암호
3. 해쉬 도구

## HMAC 동작원리

<img src="https://github.com/AI-Expo-2023/Chromatica-Client-V1/assets/100929676/3123c3fd-8858-445b-b038-4bee41c3b5ba">

1. 해쉬 생성: 클라이언트는 key + message를 HMAC 알고리즘으로 처리하여 해쉬 값을 만들어 냅니다.
2. 요청 보내기: 생성된 해쉬와 message를 HTTP 요청으로 REST API 서버에 보냅니다. 보통 해쉬는 HTTP 헤더 또는 url에 포함됩니다.
3. 해쉬 생성: 서버는 클라이언트에게서 받은 요청 내의 message와 본인이 가지고 있던 key를 조합하여 HMAC로 해쉬 값을 생성합니다.
4. 비교: 클라이언트에서 넘어온 해쉬와 서버에서 생성된 해쉬가 동일한지 비교합니다. 동일하면 인증 성공입니다.

## 구현해보기!

구현할 때 2가지 방식으로 구현할 수 있게됩니다. 첫번째는 **Hex Encode 암호화**를 통한 암호화 두번째는 **Base64 Encode 암호화**가 있습니다.

**기본적으로 필요한 것들은 아래와 같습니다.**

- 암호화에 Java 기본 라이브러리(javax.crypto.**Mac**, javax.crypto.spec.**SecretKeySpec**)를 사용합니다.
- 암호화 한 값을 출력(인코딩)을 위해 **Apache Commons** 라이브러리를 사용합니다(다운로드 필요!).

### Hex Encode 암호화

```java
import java.io.UnsupportedEncodingException;
import java.security.InvalidKeyException;
import java.security.NoSuchAlgorithmException;

import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;

import org.apache.commons.codec.binary.Hex;

public class HmacShaClass {

	public static void main(String[] args) throws InvalidKeyException, NoSuchAlgorithmException, UnsupportedEncodingException {
		
		String text = "Hmac Test Text";
		String secretKey = "Hmac Key"; 
		
		System.out.println("암호화 전: " + text);		
		
		System.out.println("-------------------------------------------------------");
		
		System.out.println("Hmac-MD5(Hex): " + HmacAndHex(secretKey, text, "HmacMD5"));
		System.out.println("Hmac-SHA1(Hex): " + HmacAndHex(secretKey, text, "HmacSHA1"));
		System.out.println("Hmac-SHA224(Hex): " + HmacAndHex(secretKey, text, "HmacSHA224"));
		System.out.println("Hmac-SHA256(Hex): " + HmacAndHex(secretKey, text, "HmacSHA256"));
		System.out.println("Hmac-SHA384(Hex): " + HmacAndHex(secretKey, text, "HmacSHA384"));
		System.out.println("Hmac-SHA512(Hex): " + HmacAndHex(secretKey, text, "HmacSHA512"));
		
		System.out.println("-------------------------------------------------------");
	}
	
	public static String HmacAndHex(String secret, String data, String Algorithms) throws NoSuchAlgorithmException, InvalidKeyException, UnsupportedEncodingException {
		
		//1. SecretKeySpec 클래스를 사용한 키 생성 
		SecretKeySpec secretKey = new SecretKeySpec(secret.getBytes("utf-8"), Algorithms);

		//2. 지정된  MAC 알고리즘을 구현하는 Mac 객체를 작성합니다.
		Mac hasher = Mac.getInstance(Algorithms);
		
		//3. 키를 사용해 이 Mac 객체를 초기화
		hasher.init(secretKey);
		
		//3. 암호화 하려는 데이터의 바이트의 배열을 처리해 MAC 조작을 종료
		byte[] hash = hasher.doFinal(data.getBytes());
		
		//4. Hex Encode to String
		return Hex.encodeHexString(hash);
	}
	
}
```

### **Base64 Encode 암호화**

```java
import java.io.UnsupportedEncodingException;
import java.security.InvalidKeyException;
import java.security.NoSuchAlgorithmException;

import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;

import org.apache.commons.codec.binary.Base64;

public class HmacShaClass {

	public static void main(String[] args) throws InvalidKeyException, NoSuchAlgorithmException, UnsupportedEncodingException {
		
		String text = "Hmac Test Text";
		String secretKey = "Hmac Key"; 
		
		System.out.println("암호화 전: " + text);		
		
		System.out.println("-------------------------------------------------------");

		System.out.println("Hmac-MD5(Base64): " + HmacAndBase64(secretKey, text, "HmacMD5"));
		System.out.println("Hmac-SHA1(Base64): " + HmacAndBase64(secretKey, text, "HmacSHA1"));
		System.out.println("Hmac-SHA224(Base64): " + HmacAndBase64(secretKey, text, "HmacSHA224"));
		System.out.println("Hmac-SHA256(Base64): " + HmacAndBase64(secretKey, text, "HmacSHA256"));
		System.out.println("Hmac-SHA384(Base64): " + HmacAndBase64(secretKey, text, "HmacSHA384"));
		System.out.println("Hmac-SHA512(Base64): " + HmacAndBase64(secretKey, text, "HmacSHA512"));
		
		System.out.println("-------------------------------------------------------");
	}
    
	public static String HmacAndBase64(String secret, String data, String Algorithms) throws NoSuchAlgorithmException, InvalidKeyException, UnsupportedEncodingException {
		
		//1. SecretKeySpec 클래스를 사용한 키 생성 
		SecretKeySpec secretKey = new SecretKeySpec(secret.getBytes("utf-8"), Algorithms);

		//2. 지정된  MAC 알고리즘을 구현하는 Mac 객체를 작성합니다.
		Mac hasher = Mac.getInstance(Algorithms);
		
		//3. 키를 사용해 이 Mac 객체를 초기화
		hasher.init(secretKey);
		
		//3. 암호화 하려는 데이터의 바이트의 배열을 처리해 MAC 조작을 종료
		byte[] hash = hasher.doFinal(data.getBytes());
		
		//4. Base 64 Encode to String
		return Base64.encodeBase64String(hash);
	}
}
```

## 안전하게 사용하기

**전송시 안전한 채널(HTTPS)을 사용**

HMAC은 secret key가 없다면 message의 위변조가 불가능하지만 원문 message를 같이 보내야 하므로 보안을 위해 HTTPS와 같이 안전한 전송 채널을 사용하는 것이 좋습니다.

**Secret key 관리**

클라이언트가 전송한 요청은 중간에 해커가 가로챌 수 있지만 secret key가 없다면 위변조해도 서버의 검증 과정에서 에러가 나게 됩니다, 반대로 secret key가 유출된다면 해커가 임의로 위변조할 수 있으므로 secret key를 안전하게 관리하고 유출 우려가 있을 경우 재발급해서 사용해야 합니다.

**Reply attach 방지**

클라이언트가 전송한 요청은 중간에 해커가 가로채서 replay attack에 활용할 수 있습니다. 그래서 전송 message에 timestamp나 serial, nonce등 변하는 값을 포함하는게 필요합니다.