---
title: "Cloud9"
weight: 22
pre: "<b>2-1. </b>"

---

### Cloud9에 Workspace를 생성할 것입니다:

AWS Cloud9은 브라우저만으로 코드를 작성, 실행 및 디버깅할 수 있는 클라우드 기반 IDE(통합 개발 환경)입니다. 코드 편집기, 디버거 및 터미널이 포함되어 있습니다. Cloud9은 JavaScript, Python, PHP를 비롯하여 널리 사용되는 프로그래밍 언어를 위한 필수 도구가 사전에 패키징되어 제공되므로, 새로운 프로젝트를 시작하기 위해 파일을 설치하거나 개발 머신을 구성할 필요가 없습니다. 

Cloud9콘솔로 가기: https://console.aws.amazon.com/cloud9

### Workspace 만들기
1. 오른쪽 상단의 **Create Environment**를 선택합니다. 
![cloud902](/images/setup/cloud9-create-environment.png)

1. Name environment의 Name에 `WellArchitectedWorkshop's Cloud9`을 입력하고 Description에는 `for Workshop`을 입력한 후 **Next Step**을 누릅니다.
![cloud903](/images/setup/cloud9-name-environment.png)

1. Configure settings는 아무것도 변경하지 않고 **Next step**을 선택합니다. 
![cloud904](/images/setup/cloud9-configure-setting.png)

{{% notice warning %}}
Cloud9을 Default환경에 배치시키세요. 실습용 VPC에 위치시키면 카오스테스트를 진행할 때 Cloud9이 종료될 수 있습니다.
{{% /notice %}}

1. Review에서 생성되는 Cloud9의 환경과 셋팅을 확인한 후 **Create Environment**를 선택합니다. 
![cloud905](/images/setup/cloud9-review.png)

1. 생성이 완료되면 아래와 같은 Cloud9이 셋팅됩니다. 
![cloud905](/images/setup/cloud9-settig-fin.png)


