### XSS(크로스 사이트 스크립팅) 방지 방법 정리<br>  
**XSS(Cross-Site Scripting)** 는 사용자가 입력한 데이터를 제대로 필터링하지 않을 경우, 공격자가 악성 스크립트를 삽입하여 실행할 수 있는 보안 취약점이다.   
이를 방지하려면 다음과 같은 방법을 활용해야 한다.  
  
## ✅ **1. 입력값 검증 및 필터링**<br>  
사용자가 입력하는 데이터에서 **스크립트 태그(<script>)나 위험한 코드**를 필터링해야 한다.  
### **🛠 Jsoup을 이용한 HTML 태그 필터링**<br>  
```java  

import org.jsoup.Jsoup;
import org.jsoup.safety.Safelist;

public class XssPrevention {
    public static void main(String[] args) {
        String unsafeHtml = "<script>alert('XSS');</script><b>안전한 태그</b>";

        // 기본적인 XSS 방어 (허용된 태그만 남김)
        String safeHtml = Jsoup.clean(unsafeHtml, Safelist.basic());

        System.out.println(safeHtml); // 출력: <b>안전한 태그</b>
    }
}

  
```  
📌 Jsoup의 clean() 메서드를 활용하면, 지정된 Safelist에 포함된 태그만 허용됨  
📌 Safelist.basic() : <b>, <i>, <u>, <strong> 등 일부 태그 허용  
  
## ✅ **2. HTML 이스케이프 처리**<br>  
출력 시, HTML 및 JavaScript를 이스케이프하여 브라우저가 코드로 해석하지 않도록 방지해야 한다.  
### **🛠 Apache Commons Text 사용 (Java)**<br>  
```java  
import org.apache.commons.text.StringEscapeUtils;

public class EscapeExample {
    public static void main(String[] args) {
        String unsafe = "<script>alert('XSS');</script>";
        String safe = StringEscapeUtils.escapeHtml4(unsafe);

        System.out.println(safe); // 출력: &lt;script&gt;alert(&#39;XSS&#39;);&lt;/script&gt;
    }
}

  
```  
📌 <script> 태그가 변환되어 실행되지 않음  
  
## ✅ **3. HTTP 응답 헤더 설정 (보안 헤더 추가)**<br>  
**XSS 공격을 브라우저에서 차단하는 보안 정책을 적용**해야 한다.  
### **🛠 Spring Security를 활용한 X-XSS-Protection 설정**<br>  
```java  
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .headers()
            .xssProtection()
            .and()
            .contentSecurityPolicy("script-src 'self'"); // 외부 스크립트 차단
    }
}

  
```  
📌 **X-XSS-Protection 활성화** : 브라우저에서 XSS 탐지 시 자동으로 차단  
📌 **CSP(Content Security Policy) 적용** :  'self'만 허용하여 외부 스크립트 실행 방지  
  
## ✅ 4**. JavaScript에서  innerHTML 대신 textContent 사용**<br>  
JavaScript로 DOM을 조작할 때, innerHTML을 사용하면 악성 스크립트가 실행될 수 있음. 대신 textContent 사용 권장.  
```javascript  
// ❌ XSS 취약 코드
document.getElementById("output").innerHTML = userInput;

// ✅ 안전한 코드
document.getElementById("output").textContent = userInput;  
```  
  
