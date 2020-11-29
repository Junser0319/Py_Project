**줌 채팅 출석체크에 대비하는 매크로 프로그램**

# 📌 Scenario

특정 과목을 줌으로 실시간 수강할 때 교수님이 학생들이 잘 듣고 있는지 간간히 채팅으로 출석한다는 내용을 올린다.

그 시간을 정확히 알 수 없으니 화장실을 갈 때나 딴 짓을 할 때, 걸리는 경우가 허다하다.

이 상황을 극복할 수 있는 스크립트를 짜보자.

## 📌 Used Main Librarys

1. 출석이라는 단어를 캐치할 `pyautogui`
2. 출석이라는 단어를 캐치한 후 채팅창에 대답까지 완료해 줄 `keyboard`

### 📌 Code Explanation

```python
while 1:
    if int(time.time()) >= stop:
        print(f"서버 과부하 우려로 스크립트 종료\n총 시도 횟수: {count}")
        sys.exit(-1)
```

main 메서드에서 스크립트가 지속될 시간을 입력받고 스크립트가 작동한 시간이 허용 시간을 넘겼다면 강제로 종료시킨다.

```python
    else:
        check = pag.locateOnScreen('attendance.PNG')
        if not check == None:
            i = pag.locateOnScreen('message_box.PNG')
            if not i == None:
                pag.screenshot('new_message_box.PNG', region=list(i))
                location = pag.locateCenterOnScreen('new_message_box.PNG')

                break
            else:
                print(f"{count}. 일치하는 이미지 없음")
                count += 1
        else:
            print(f"{count}. 일치하는 이미지 없음")
            count += 1
```

출석이라는 단어를 찾고 사용자마다 채팅창의 위치는 다를 수 있기에 초기에 준 채팅창 이미지를 스캔한 후 새로운 위치를 가져온다.

```python
    time.sleep(2)
```

스크립트를 구동하는 로컬 혹은 서버가 while 문에 의해 과부하되지 않도록 2초 동안의 시간을 준다.


#### 📌 작동 움짤

![image_Zoom_Attendance](image/image_Zoom_Attendance.gif)
