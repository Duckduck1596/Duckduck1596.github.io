#파일 변화 모니터링하기

- 특정 디렉토리(monitor_dir)를 실시간 모니터링하면서 새로운 파일이 추가되면 자동으로 감지하고 감지된 파일을 열어서 이메일 주소나 주석(# 또는 //로 시작하는 라인)을 찾아 출력.


```
import os
import time
import re

# 모니터링 디렉토리 설정
MONITOR_DIR = "monitor_dir"

#od.listdir -> 폴더안에 파일 목록 가져옴 set() 묶는 이유는 집합 연산을 하기 위함(새로운 파일 감지를 위함)
pre_files = set(os.listdir(MONITOR_DIR))

#이메일과 주석을 탐지하기위한 패턴 설정
detect_email = re.compile(r"[a-zA-Z0-9_.+-]+@[a-zA-Z0-9_.+-]+\.[a-zA-Z0-9_.+-]+")
detect_commentn = re.compile(r"^\s*(#|//).*")

print(f"모니터링 시작: {MONITOR_DIR}")
print(f"초기 파일 목록: {pre_files}")

#새로운 파일 모니터링
while True:
    try:
        current_files = set(os.listdir(MONITOR_DIR))
        new_files = current_files - pre_files

        #새 파일 있으면 출력
        if new_files:
            for filename in new_files:
                filepath = os.path.join(MONITOR_DIR, filename)
                print(f"\n 새로운 파일 추가 감지: {filename}")

                # 파일을 읽고 이메일, 주석 확인. enumerate(f, start=1):는 줄번호를 함께 가져옴.
                try:
                    with open(filepath, "r", encoding="utf-8") as f:
                        for i, line in enumerate(f, start=1):
                            if detect_email.search(line):
                                print(f"이메일 발견 {filename}:{i} -> {line.strip()}")
                            if detect_commentn.search(line):
                                print(f"주석 발견 {filename}:{i} -> {line.strip()}")
    
                # 파일을 열 수 없으면 출력
                except Exception as e:
                    print(f"오류 {filename} 파일을 열 수 없음: {e}")

        #현재 파일 목록을 기준값으로 업데이트, 1초 대기 후 다시 확인.
        pre_files = current_files
        time.sleep(1)

    #CTRL+C 모니터링 종료
    except KeyboardInterrupt:
        print("\n 모니터링 종료")
        break
```