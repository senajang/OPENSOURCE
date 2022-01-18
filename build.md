# Travis CI
- CI 서비스 중 하나로, 깃헙에 호스팅 되는 소프트웨어 프로젝트의 빌드, 테스트를 위해 사용된다.
- 코드 수정 -> PR -> 테스트 코드 실행, 코드 검증 (Travis CI) -> Approve -> Merge의 과정으로 작동된다.

## Travis 사용 방법
1) Travis와 github를 연동한다.
2) travis.yml 파일을 프로젝트에 추가한다.   
ex)
```
language: android
sudo: required
language: android
jdk: oraclejdk11

dist: trusty

android:
  licenses:
    - 'android-sdk-preview-license-.+'
    - 'android-sdk-license-.+'
    - 'google-gdk-license-.+'

  components:
    - tools
    - build-tools-30.0.2
    - android-30
    - android-22
    - extra-google-google_play_services
    - extra-google-m2repository
    - extra-android-m2repository
    - sys-img-armeabi-v7a-android-22

before_install:
  - chmod +x gradlew
  - yes | sdkmanager "platforms;android-30"

before_script:
  - echo no | android create avd --force -n test -t android-22 --abi armeabi-v7a
  - emulator -avd test -no-audio -no-window &
  - android-wait-for-emulator
  - adb shell input keyevent 82 &

script:
  - ./gradlew clean build
  - ./gradlew test
  - ./gradlew build check
  ```

