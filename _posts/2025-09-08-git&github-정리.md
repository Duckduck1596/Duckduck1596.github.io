# Git & GitHub 정리 (윈도우 기준)

## 1. Git & GitHub란?
- **Git**: 소스코드 변경 이력을 추적·관리하는 분산 버전 관리 시스템(VCS).
- **GitHub**: Git 저장소를 원격으로 호스팅하고 협업(이슈, PR, 코드리뷰 등)을 지원하는 플랫폼.
> 정리: Git은 도구, GitHub은 그 도구를 올려 협업하는 서비스.

---

## 2. Git 설치하기 (윈도우)
1) https://gitforwindows.org 에서 설치 파일 다운로드  
2) 기본 옵션으로 설치(깃 배시 포함)  
3) 설치 확인
```bash
git --version
```

---

## 3. 사용자 정보 설정

```
git config --global user.name "김대한"
git config --global user.email "your_email@example.com"
git config --list
```

---
## 4. 새 프로젝트 시작(로컬에서 처음 만드는 경우) — git init 사용

#### 0. (선택) 새 저장소의 기본 브랜치를 main으로 하고 싶다면 한 번만 설정
```
git config --global init.defaultBranch main
```

#### 1. 작업 폴더 생성 후 진입
```
mkdir my-project && cd my-project
```
#### 2. Git 초기화
```
git init
```
#### 3. (선택) README와 .gitignore 생성
```
echo "# my-project" > README.md
#### 예: Node라면
#### echo "node_modules/" > .gitignore
```

#### 4. 첫 커밋
```
git add .
git commit -m "chore: initial commit"
```

#### 5. GitHub에서 빈 원격 저장소 생성 후, 원격 추가
#### (아래 경로를 본인 것으로 변경)
```
git remote add origin git@github.com:username/my-project.git
```

#### 6. 브랜치명이 master라면 main으로 변경(또는 위에서 init.defaultBranch 설정을 사용)
```
git branch -M main
```
#### 7. 최초 푸시(업스트림 설정)
```
git push -u origin main
```

#### 이후 반복: 작업 -> add -> commit -> push


## 5. 기존 원격 저장소로 시작(이미 GitHub에 저장소가 있는 경우) — git clone 사용


#### 1. 원격 저장소를 로컬로 복제
```
git clone git@github.com:username/repository.git
cd repository
```

#### 2. 작업 상태 확인
```
git status
```

#### 3. 스테이징 -> 커밋 -> 푸시
```
git add .
git commit -m "feat: update something"
git push origin main
```

#### 4. 원격 변경 동기화
```
git pull origin main      # 가져오며 자동 병합
git fetch origin          # 변경만 가져오고 병합은 수동
```
**핵심 정리**

- 새 저장소를 로컬에서 처음 만들 때 → git init

- 이미 GitHub에 저장소가 있을 때 → git clone

- git clone으로 가져온 폴더 안에서는 다시 git init을 실행하지 않습니다(중첩 저장소 문제 발생).

---

## 6. 자주 쓰는 Git 명령어 예시
```

git log --oneline --graph --decorate --all   # 로그 요약
git diff                                     # 변경 비교
git branch                                   # 브랜치 목록
git checkout -b feature/new-stuff            # 새 브랜치 생성/이동
```
#### 작업

```
git add .
git commit -m "feat: add new stuff"
git switch main || git checkout main         # 메인으로 이동
git merge feature/new-stuff                  # 브랜치 병합
```


# 7. 전체 흐름 요약(명령으로 재정리)
```
git --version
git config --global user.name "김대한"
git config --global user.email "your_email@example.com"
git clone git@github.com:username/repository.git
cd repository
git add .
git commit -m "메시지"
git push origin main
git pull origin main
git fetch origin
```