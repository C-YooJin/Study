### About Commit log
- [좋은 git commit message를 작성하기 위한 8가지 약속](https://djkeh.github.io/articles/How-to-write-a-git-commit-message-kor/)
- [좋은 git commit message를 위한 영어 사전](https://blog.ull.im/engineering/2019/03/10/logs-on-git.html)
- [간결한 commit message(실제 소동물 분양 사이트 개발 리포에서 쓰고 있음)](https://blog.ull.im/engineering/2019/03/10/logs-on-git.html)

### LF will be replaced by CRLF in some/file.file. 이런 에러가 나타나는 경우
- 이러한 에러는 윈도우와 유닉스체제간의 협업을 할 때 주로 발생함. white space 에러고, 유닉스 시스템에서는 한 줄의 끝이 LF(Line Feed)로 이루어지는 반면, 윈도우에서는 줄 하나가 CR(Carriage Return)와 LF(Line Feed), 즉 CRLF로 이루어지기 때문임. 윈도우와 유닉스 시스템에서 이러한 white space 호환을 자유롭게 해주려면 간단한 명령어 필요
- `git config --global core.autocrlf true`
- 이 명령어를 입력해주면 자동으로 CR과 LF를 변환해준다.
