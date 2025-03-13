### **🐳 Docker 간략한 설명**<br>  
Docker는 컨테이너 기술을 활용하여 애플리케이션을 가볍고, 이식 가능하며, 일관된 환경에서 실행할 수 있도록 해주는 가상화 도구  
•	기존의 **VM(가상 머신)** 과 달리, OS 전체를 가상화하지 않고 **애플리케이션과 필요한 라이브러리만 컨테이너로 패키징**하여 실행  
•	개발, 테스트, 운영 환경 간의 불일치를 해결하여 **CI/CD 및 DevOps에 최적화**  
•	**“한 번 빌드하면 어디서든 실행 가능”**  
  
### **Docker Compose 올리기 & 내리기**<br>  
```docker  
docker-compose up -d   # 실행
docker-compose down    # 중지 및 삭제  
```  
  
### 예시<br>  
1. 프로젝트 루트폴더에 docker를 설치  
1. docker-compose.yml을 셋팅한 후 올리면 컨테이너 실행 완료  
![IMAGE](https://raw.githubusercontent.com/nogi-bot/resources/main/gwkcareer/images/48d25e72-ed1b-4f68-87c6-19d0fc5db950-image.png)  
