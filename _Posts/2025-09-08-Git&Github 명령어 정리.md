# 🖥️ Git & GitHub 완전 정리 (윈도우 기준)

개발을 하다 보면, 코드 버전 관리와 협업이 필수적입니다.  
이때 가장 많이 쓰이는 도구가 바로 **Git**과 **GitHub** 입니다.  

오늘은 제가 공부한 **Git & GitHub 설치, 설정, 기본 사용법, 단축 명령어**까지 블로그 스타일로 정리해보겠습니다.

---

## 1. Git & GitHub란?

- **Git**  
  소스코드를 관리하는 **버전 관리 시스템(VCS, Version Control System)**  
  👉 코드 변경 내역을 추적하고, 과거 기록으로 쉽게 돌아갈 수 있음.  

- **GitHub**  
  Git 저장소를 **원격(클라우드)**에 올려두고 관리할 수 있는 플랫폼  
  👉 혼자 쓰기에도 좋고, 팀 프로젝트 협업에 필수적임.  

> 쉽게 말해, **Git은 도구, GitHub은 그 도구를 저장하고 공유하는 서비스**라고 이해하면 됩니다.

---

## 2. Git 설치하기 (윈도우)

1. [Git for Windows 공식 사이트](https://gitforwindows.org/)에서 설치 파일 다운로드  
2. 설치 시 기본 옵션으로 진행 → **Git Bash** 터미널도 함께 설치됨  
3. 설치 완료 후, Git Bash 실행 → 아래 명령어로 확인
    ```bash
    git --version
    ```
    ✅ 버전이 출력되면 설치 성공!

---

## 3. 사용자 정보 설정

Git은 커밋할 때마다 **누가 작성했는지** 기록을 남깁니다.  
따라서 처음 한 번은 사용자 정보를 등록해야 합니다.  

```bash
git config --global user.name "name"
git config --global user.email "your_email@example.com"

#설정 확인
git config --list
```


