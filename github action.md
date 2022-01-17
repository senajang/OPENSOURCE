# github action이란?
- 소프트웨어 개발 workflow를 repository에서 바로 자동화, 사용자 지정 및 실행할 수 있도록 해주는 도구이다.    
- Github Action은 **workflow, events, runner, jobs, step, action**으로 구성되어 있다.
1. **Workflow**
- 여러 job으로 구성되고, event에 의해 실행 될 수 있는 자동화된프로세스
- YAML로 작성되고, github/workflows 폴더 내에 .yml파일을 추가하여 등록 할 수 있음.
2. **Event**
- workflow를 실행하는 특정 활동이나 규칙
- ex) 특정 브랜치로 push, 특정 브랜치로 pull request 등
3. **Runner**
- Gitbub Action Runner 어플리케이션이 설치된 머신으로, Workflow가 실행될 인스턴스
4. **Job**
- job은 여러 step으로 구성되어 있고, 가상 환경의 인스턴스에서 실행됨
5. **Step**
- task들의 집합으로 커맨드를 날리거나 action을 실행 할 수 있음
6. **action**
- Workflow의 가장 작은 블럭(smallest portable building block)
- Job을 만들기 위해 Step들을 연결할 수 있음
- 재사용이 가능한 컴포넌트
- 개인적으로 만든 Action을 사용할 수도 있고, Marketplace에 있는 공용 Action을 사용할 수도 있음

## CI/CD
- CI/CD는 Continuous integration and continuous delivery의 약자로 '지속적인 통합 및 지속적인 제공'이라고 번역된다. 

# commit message check
## commit message check의 목적
commit message에 대한 규칙을 만들어 관리하면서 commit message에 대한 가독성을 높이기 위하여
## commit message 적용 방법
1. commit message template을 작성하여 gitmessage.txt로 저장한다.    
<pre><code>{###############################################################
# Commit Message Template
###############################################################

# type : subject
# Subject 50 characters


# Body Message
# Body 72 characters(부연설명)


# footer (이슈를 추적하기 위한 이슈번호)
# Issue Tracker Number  ex) issue #1

###############################################################
# Rememver ME Commit Message 
###############################################################

#### type 에는 다음과 은 단어가 들어가도록한다. ####
# Feat	        새로운 기능을 추가할 경우
# Fix	        버그를 고친 경우
# Design	    CSS 등 사용자 UI 디자인 변경
# Style	        코드 포맷 변경, 세미 콜론 누락, 코드 수정이 없는 경우
# Refactor	    프로덕션 코드 리팩토링
# Comment	    필요한 주석 추가 및 변경
# Docs	        문서를 수정한 경우
# Test	        테스트 추가, 테스트 리팩토링(프로덕션 코드 변경 X)
# Chore 	    빌드 태스트 업데이트, 패키지 매니저를 설정하는 경우(프로덕션 코드 변경 X)
# Rename	    파일 혹은 폴더명을 수정하거나 옮기는 작업만인 경우
# Remove	    파일을 삭제하는 작업만 수행한 경우}</code></pre>
2. (전역 설정) git config --global commit.template <.gitmessage.txt 경로>
(Repository마다 다르게 설정) git config commit.template <.gitmessage.txt 경로>
3. 설정 완료 후 git init -> git add . -> git commit(형식에 맞춰 작성) -> git push 과정으로 사용   

# CLA란 무엇인가?   
- CLA는 Contributor License Agreement의 약자로 번역하면 기여자 라이선스 동의이다.   
- CLA를 사용하면 기여자 들이 저작권 분쟁에 따른 법적 해결책을 쉽게 준수하게 할 수 있다.    
- 서드파티가 기여를 수여한 제품의 리라이선스(relicense)를 가능케 한다.    
- CLA는 모든 오픈소스 프로젝트에 CLA를 추가할 필요는 없다. 그러나 카피레프트 라이선스를 다르는 기업 오픈 소스 프로젝트들에게 중요한데, 그 이유는 CLA 없이는 기여자 또한 제한을 두기 때문이다.
- CLA의 목적은 프로젝트 산물의 기여자가 모든 기여에 대해 필요한 소유권이나 권한을 가질 수 있도록 보장함으로써 이들이 선택한 라이선스 - 하에 배포하는 것을 가능케 한다.
# CLA Check
.github/workflows/cla.yml 파일 예시
```
name: "CLA Assistant"
on:
  issue_comment:
    types: [created]
  pull_request_target:
    types: [opened,closed,synchronize]

jobs:
  CLAssistant:
    runs-on: ubuntu-latest
    steps:
      - name: "CLA Assistant"
        if: (github.event.comment.body == 'recheck' || github.event.comment.body == 'I AGREE this CLA') || github.event_name == 'pull_request_target'
        # Beta Release
        uses: cla-assistant/github-action@v2.1.3-beta
        env:
          GITHUB_TOKEN: ${{ secrets.TOKEN }}
          # the below token should have repo scope and must be manually added by you in the repository's secret
          PERSONAL_ACCESS_TOKEN : ${{ secrets.PERSONAL_ACCESS_TOKEN }}
        with:
          path-to-signatures: 'cla/signatures/version1/cla.json'
          path-to-document: 'https://github.com/senajang/SSIUM_UMBRELLA_RENTSYSTEM/blob/master/cla/cla.md' # e.g. a CLA or a DCO document
          # branch should not be protected
          branch: 'master'
          allowlist: bot*

         #below are the optional inputs - If the optional inputs are not given, then default values will be taken
          ##remote-organization-name: enter the remote organization name where the signatures should be stored (Default is storing the signatures in the same repository)
          ##remote-repository-name:  enter the  remote repository name where the signatures should be stored (Default is storing the signatures in the same repository)
          #create-file-commit-message: 'For example: Creating file for storing CLA Signatures'
          #signed-commit-message: 'For example: $contributorName has signed the CLA in #$pullRequestNo'
          custom-notsigned-prcomment: "\n\n프로젝트에 기여해 주셔서 감사합니다! 요청해 주신 PR을 반영하기 이전에, [Contributor License Agreements](https://ko.wikipedia.org/wiki/%EA%B8%B0%EC%97%AC%EC%9E%90_%EB%9D%BC%EC%9D%B4%EC%84%A0%EC%8A%A4_%EB%8F%99%EC%9D%98)에 동의해 주셔야 합니다. [해당 문서](https://github.com/senajang/SSIUM_UMBRELLA_RENTSYSTEM/blob/master/cla/cla.md)를 확인하신 후, 댓글로 아래 문구(I AGREE this CLA)를 남겨주시면 CLA 사인이 완료됩니다.\n\nThank you for your pull request and welcome to our community! We require contributors to sign our [Contributor License Agreement](https://en.wikipedia.org/wiki/Contributor_License_Agreement). After checking [this document](https://github.com/gon1942/test/blob/master/cla/cla.md), please leave the following statement(I AGREE this CLA) in the comments to complete the CLA signature."
          custom-pr-sign-comment: 'I AGREE this CLA.'
          #custom-allsigned-prcomment: 'pull request comment when all contributors has signed, defaults to **CLA Assistant Lite bot** All Contributors have signed the CLA.'
          #lock-pullrequest-aftermerge: false - if you don't want this bot to automatically lock the pull request after merging (default - true)
          #use-dco-flag: true - If you are using DCO instead of CLA

```

