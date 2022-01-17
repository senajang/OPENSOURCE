# issue란?
issue는 프로젝트의 작업, 개선 사항 및 버그를 추적하는 좋은 방법으로 사용된다.    
프로젝트 기획, 새롭게 추가될 기능, 버그와 수정 사항 모든 것을 이슈라고 할 수 있다.
## issue flow
1. issue 등록
2. issue 작업
3. pull request&code review
4. issue 반영&

# issue label
issue label은 issue의 카테고리를 한눈에 알아보기 쉽게 하기 위하여 만들어진다.   
## 대표적인 issue label의 종류   
|keyword|의미|  
|--------|---|   
|bug|예기치 않은 문제 또는 의도하지 않은 동작(버그)을 나타냅니다.|
|documentation|문서를 개선하거나 추가 할 필요가 있음을 나타냅니다.|
|duplicate|해당이슈 또는 PR이 기존에 있음을 나타냅니다.|
|enhancement|새로운 기능 요청을 나타냅니다.|
|good first issue|처음 기여해볼 사람에게 좋은 문제를 나타냅니다.|
|help wanted|관리자가 문제 또는 PR 요청에 대한 도움을 원함을 나타냅니다.|
|invalid|이슈 또는 PR 요청이 더 이상 관련이 없음을 나타냅니다.|
|question|이슈 또는 풀 요청에 추가 정보가 필요함을 나타냅니다.|
|wontfix|문제나 PR 요청에서 작업이 계속되지 않음을 나타냅니다.|

# issue template
issue의 제목, 내용을 중구난방으로 작성하지 않고 정해진 틀 안에서 작성하여 더욱 알아보기 쉽게 하기 위하여 issue template을 사용한다.   

## issue template 설정 방법
1. repository에서 settings를 클릭한다.
2. features의 issues칸에서 set up templates 버튼을 클릭한다.
3. 원하는 형식으로 issue templates을 수정하고 commit한다.   
ex)   
```
### 개요 ###
- 내용을 적어주세요
### 이슈 종류를 선택해주세요 ###
[-] New Feature
[ ] Bug Fix

### 내용 ###
-  이슈 종류가 버그일 경우 어떤식으로 버그가 발생했는지 적어주세요.

### Type List ###
bug : Something isn't working
documentation : Improvements or additions to documentation
duplicate : This issue or pull request already exists
enhancement : new feature or request 
help wanted : Extra attention is needed
invalid : This doesn't seem right
question : Further information is requested
wontfix : This will not be worked on
```
 
# milestone
프로젝트를 효과적으로 관리하기 위하여 연관된 issue들을 milestone으로 분류하여 나타낼 수 있다.   
milestone은 **마감일, 완료율, open된 issue의 수, closed issue의 수, pull request의 수**를 표기 해줘서 효율적으로 project관리를 할 수 있게 해준다.

# project
Project Board는 다양한 이슈를 관리할 수 있는 Kanban Board와 같은 개념이다.   
**ToDo** - 처리해야할 issue에 대하여 표기   
**In Progress**  - 현재 진행중인 Issue들을 ToDo에서 표기   
**Done** - 완료된 Issue를 표기

