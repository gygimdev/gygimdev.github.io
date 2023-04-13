# 자바 설치하기
- 자바 15 까지는 home brew 통해서 설치 가능
```
brew update
brew tap adoptopenjdk/openjdk
brew search jdk
brew install --cask adoptopenjdk11
brew install --cask adoptopenjdk14
```

- 16 부터는 AdoptOpenJDK 프로젝트 명이 Adoptium 으로 변경 되었다.
```
brew tap homebrew/cask-versions
brew install --cask temurin17
```

# 자바 버전 확인 
``` shell
java --version
```

# 자바가 설치된 곳 확인
``` shell
/usr/libexec/java_home -V
```

# 자바 버전 바꾸기
``` shell
vi ~/.zshrc
```

입력할 내용
``` shell
# Java Paths
export JAVA_HOME_11=$(/usr/libexec/java_home -v11)
export JAVA_HOME_14=$(/usr/libexec/java_home -v14)

# Java 11
export JAVA_HOME=$JAVA_HOME_11

# Java 14
# 14버전을 사용하고자 하는 경우 아래 주석(#)을 해제하고 위에 11버전을 주석처리 하면된다.
# export JAVA_HOME=$JAVA_HOME_14
```

쉘에 변경사항 반영
```
source ~/.zshrc
```


