#숫자 맞추기 게임 만들기

오늘은 파이썬 예전에 공부했을 때 만들어본 숫자 맞추기 게임을 다시 만들어 보았습니다.

```
import random

def number_guessing_game():
    print("숫자 맞추기 게임에 오신 것을 환영합니다!")
    print("1부터 100 사이의 숫자를 맞춰보세요.")

    # 1부터 100 사이의 랜덤 숫자 생성
    number_to_guess = random.randint(1, 100)
    attempts = 0 # 시도 횟수 기록

    while True:
        try:
            # 사용자 입력
            user_guess = int(input("숫자를 입력하세요: "))
            attempts += 1

            # 비교 후 힌드 제공
            if user_guess < number_to_guess:
                print("너무 낮아요! 다시 시도해보세요.")
            elif user_guess > number_to_guess:
                print("너무 높아요! 다시 시도해보세요.")
            else:
                # 정답 일 경우 게임 종료
                print(f"정답입니다! {attempts}번 만에 맞추셨습니다.")
                break
        except ValueError:
            print("숫자를 입력해주세요.")

while True:
    number_guessing_game()
    play_again = input("다시 하시겠습니까? (y/n): ").strip().lower()
    if play_again != 'y':
        print("게임을 종료합니다. 감사합니다!")
        break

```

조금 더 다양한 기능을 만들 수 있었지만 PBL에 중어진 조건에 한에 만들어 보았습니다 오랜만에 다시 만드니 코드도 깔끔해진거 같고 쉽게 느껴져 그래도 공부한 성취감을 조금 느꼈습니다 하루하루 발전하는 내가 되길 바랍니다.