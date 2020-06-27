## Python

### GIL(Global Interpreter Lock)
Python에서 멀티 쓰레드를 동작시키면, (쓰레드가 늘어날수록) 실행속도가 더 늘어나는 이상한 현상이 보인다. 그 이유는 파이썬의 GIL때문이다. 파이썬이 GIL을 사용하기 떄문
이다. 쉽게 말해 멀티 쓰레드로 구현했어도, 싱글 쓰레드로 밖에 사용을 못 하는 것이다
. 왜 그럴까? 파이썬은 GIL때문에 한 CPU당 하나의 작업밖에 할 수 없게 한다. 만약 1번
 스레드가 GIL을 잡고 작업을 하다가, 파일 IO나 네트워크 IO를 발생시키면 2번 스레드>가 GIL을 잡고 자신의 작업을 실행시킨다. 마찬가지로 2번 스레드가 파일IO나 네트워크IO를 발생시키면 3번이나 1번이나 여튼 상황에 맞게 다른 스레드가 GIL을 잡고(Context Switch(문맥 전환)라고 한다) 작업을 실행시킨다. 즉 각 스레드가 원하는 시점에 GIL을 >잡지 못하면, 작업이 지연된다는 소리다. 만약 부득이하게 IO가 발생하더라도 계속 작업
을 진행해야 한다면 Py_BEGIN_ALLOW_THREADS를 사용하면 된다. (강제 GIL 조작). GIL은 랜덤으로 할당됨. 동시성과 병렬성이 다르다는 것 잘 알아야 되고. 그렇다면 파이썬에서
 병렬성을 포기해야 하는가? -> NOPE. Multiprocessing을 쓰면 된다. </br>
파이썬의 이러한 점에도 불구하고 최근 각광받는 이유는?</br>
1. 분산처리가 발전하면서 한 컴퓨터내의 자원에 묶일 필요가 없다.
2. 하드웨어의 발전으로 네트워크 I/O가 프로그램 지연의 대부분을 차지하기 때문이다.

#### Ref.
- [Python GIL](https://medium.com/@mjhans83/python-gil-f940eac0bef9) </br>
- [Python에서의 동시성, 병렬성](https://www.slideshare.net/deview/2d4python) </br

### Celery
Celery는 메시지 패싱 방식의 <b>"분산 비동기 작업 큐(Asynchronous task queue/job queue)"</b>다. 작업(Task)은 브로커(Broker)를 통해 메시지(Message)로 워커(Worker)에 >전달되어 처리된다. 작업은 멀티프로세싱, eventlet, gevent 를 사용해 하나 혹은 그 이
상의 워커에서 동시적으로 실행되며 백그라운드에서 비동기적으로 실행될 수 있다.

#### Ref.
- [[번역] 샐러리 입문하기](https://beomi.github.io/2017/03/19/Introduction-to-Celery/)
- [Django + celery + Redis 이용하기](https://whatisthenext.tistory.com/127)
>
