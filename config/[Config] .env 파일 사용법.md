## 1. .env 파일이란?  
.env 파일은 환경 변수(Environment Variables)를 정의하는 파일로, docker-compose.yml과 함께 사용하여 민감한 정보를 숨기거나 설정 값을 관리할 수 있음.  
  
## 2. .env 파일 생성 및 사용  
  
## 3. .env 파일 관리 시 주의사항  
* 프로젝트 루트 디렉토리에 .env 파일 생성  
* .gitignore에 추가 .env 파일에는 비밀번호, API 키 등의 민감한 정보가 포함될 수 있으므로, .gitignore에 추가하여 Git에 업로드되지 않도록 설정  
* 환경 변수 값에 특수 문자 포함 시 따옴표 사용  
