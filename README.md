# Study for my dev life :pencil2::green_heart:

## About Commit log 
- [좋은 git commit message를 작성하기 위한 8가지 약속](https://djkeh.github.io/articles/How-to-write-a-git-commit-message-kor/)
- [좋은 git commit message를 위한 영어 사전](https://blog.ull.im/engineering/2019/03/10/logs-on-git.html)


## big-O 표기법
- [자료구조, 알고리즘 - 성능측정(big-O)](https://wayhome25.github.io/cs/2017/04/20/cs-26-bigO/)
- [빅오 표기법](https://cjh5414.github.io/big-o-notation/)

## Python
### 프로세스(Process)란? 
프로세스(process)란 단순히 실행 중인 프로그램(program)이다. 즉, 사용자가 작성한 프로그램이 운영체제에 의해 메모리 공간을 할당받아 실행 중인 것을 말한다. 이러한 프로세스는 프로그램에 사용되는 데이터와 메모리 등의 자원 그리고 스레드로 구성된다.

### 스레드(Thread)란?
스레드(thread)란 프로세스(process) 내에서 실제로 작업을 수행하는 주체를 의미한다. 모든 프로세스에는 한 개 이상의 스레드가 존재하여 작업을 수행한다. 또한, 두 개 이상의 스레드를 가지는 프로세스를 멀티스레드 프로세스(multi-threaded process)라고 한다.

### GIL(Global Interpreter Lock)
Python에서 멀티 쓰레드를 동작시키면, (쓰레드가 늘어날수록) 실행속도가 더 늘어나는 이상한 현상이 보인다. 그 이유는 파이썬의 GIL때문이다. 파이썬이 GIL을 사용하기 떄문이다. 쉽게 말해 멀티 쓰레드로 구현했어도, 싱글 쓰레드로 밖에 사용을 못 하는 것이다. 왜 그럴까? 파이썬은 GIL때문에 한 CPU당 하나의 작업밖에 할 수 없게 한다. 만약 1번 스레드가 GIL을 잡고 작업을 하다가, 파일 IO나 네트워크 IO를 발생시키면 2번 스레드가 GIL을 잡고 자신의 작업을 실행시킨다. 마찬가지로 2번 스레드가 파일IO나 네트워크IO를 발생시키면 3번이나 1번이나 여튼 상황에 맞게 다른 스레드가 GIL을 잡고(Context Switch(문맥 전환)라고 한다) 작업을 실행시킨다. 즉 각 스레드가 원하는 시점에 GIL을 잡지 못하면, 작업이 지연된다는 소리다. 만약 부득이하게 IO가 발생하더라도 계속 작업을 진행해야 한다면 Py_BEGIN_ALLOW_THREADS를 사용하면 된다. (강제 GIL 조작). GIL은 랜덤으로 할당됨. 동시성과 병렬성이 다르다는 것 잘 알아야 되고. 그렇다면 파이썬에서 병렬성을 포기해야 하는가? -> NOPE. Multiprocessing을 쓰면 된다.

#### Ref.
[Python GIL](https://medium.com/@mjhans83/python-gil-f940eac0bef9) </br>
[Python에서의 동시성, 병렬성](https://www.slideshare.net/deview/2d4python) </br>

### 동시성과 병렬성

