Jsoup은 실제 HTML 작업을 위한 Java 라이브러리이다.  
## **📌 Jsoup의 주요 기능**<br>  
### ✅ **1. HTML 문서 파싱 및 조작**<br>  
* HTML 문서를 Java 객체처럼 다룰 수 있음.  
* 특정 요소를 찾아서 수정하거나 삭제 가능.  
### ✅ **2. 웹 스크래핑 (크롤링)**<br>  
* Jsoup을 이용하면 웹 페이지의 데이터를 가져와서 활용할 수 있음.  
* 웹 사이트에서 특정 태그의 내용을 쉽게 추출 가능.  
### ✅ **3. XSS 방지 (HTML 정리)**<br>  
* Jsoup을 이용해 **스크립트 태그**나 **악성 코드**를 자동으로 제거 가능.  
* 보안상 중요한 웹 에디터나 사용자 입력 필터링에 활용.  
  
  
(✅ **HTML 파싱 및 조작 + 웹 스크래핑 + XSS 방지**)  
```java  
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;
import org.jsoup.safety.Safelist;

public class JsoupFullExample {
    public static void main(String[] args) throws Exception {
        // 📌 1️⃣ 웹 스크래핑 (네이버 뉴스 페이지에서 제목 가져오기)
        String url = "https://news.naver.com/";
        Document doc = Jsoup.connect(url).get();

        // 제목 목록 가져오기
        Elements headlines = doc.select("a"); // 모든 링크(<a>) 태그 가져오기
        System.out.println("📢 네이버 뉴스 주요 제목:");
        for (int i = 0; i < 5; i++) { // 상위 5개만 출력
            System.out.println("- " + headlines.get(i).text());
        }

        // 📌 2️⃣ HTML 파싱 및 조작 (문서에서 특정 요소 수정)
        String html = "<html><body><h1>원래 제목</h1><p>내용</p></body></html>";
        Document localDoc = Jsoup.parse(html);

        // <h1> 태그 변경
        Element h1 = localDoc.selectFirst("h1");
        if (h1 != null) {
            h1.text("Jsoup을 사용하여 제목 변경 완료!");
        }

        System.out.println("\n📌 HTML 파싱 및 조작 결과:");
        System.out.println(localDoc.html()); // 수정된 HTML 출력

        // 📌 3️⃣ XSS 방지 (사용자 입력 필터링)
        String unsafeInput = "<script>alert('XSS 공격!');</script><b>안전한 텍스트</b>";

        // XSS 필터링 적용
        String safeOutput = Jsoup.clean(unsafeInput, Safelist.basic());

        System.out.println("\n🔒 XSS 필터링 결과:");
        System.out.println(safeOutput); // <script> 태그가 제거된 안전한 HTML 출력
    }
}
  
```  
