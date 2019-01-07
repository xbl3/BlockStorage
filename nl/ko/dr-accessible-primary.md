---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-10"

---
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}

# 재해 복구 - 액세스 가능한 1차 볼륨으로 장애 복구

1차 사이트에서 파국적 장애나 재해가 발생하고 1차 스토리지에는 여전히 액세스할 수 있는 경우 고객은 다음의 조치를 취하여 2차 사이트의 데이터에 빠르게 액세스할 수 있습니다. 

장애 복구를 시작하기 전에 모든 호스트 권한 부여가 준비되어 있는지 확인하십시오.

권한 부여된 호스트 및 볼륨은 동일한 데이터 센터에 있어야 합니다. 예를 들어 복제본 볼륨은 런던에 두고 호스트는 암스테르담에 둘 수는 없습니다. 둘 다 런던에 있거나 둘 다 암스테르담에 있어야 합니다.
{:note}

1. [{{site.data.keyword.cloud}} 콘솔 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://
{DomainName}/catalog/){:new_window}에 로그인하고 왼쪽 상단에서 **메뉴** 아이콘을 클릭하십시오. **클래식 인프라**를 선택하십시오.

   또는 [{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}에 로그인할 수 있습니다.
2. **{{site.data.keyword.blockstorageshort}}** 페이지에서 소스 또는 대상 볼륨을 클릭하십시오.
3. **복제본**을 클릭하십시오.
4. **호스트 권한 부여** 프레임으로 스크롤하고 오른쪽에 있는 **호스트 권한 부여**를 클릭하십시오.
5. 복제에 대해 권한 부여되는 호스트를 강조표시하십시오. 호스트를 여러 개 선택하려면 CTRL 키를 사용하고 해당 호스트를 클릭하십시오.
6. **제출**을 클릭하십시오. 사용 가능한 호스트가 없는 경우 같은 데이터 센터에서 컴퓨팅 리소스를 구매하도록 프롬프트가 표시됩니다.


## 볼륨에서 복제본으로 장애 복구 시작

장애 이벤트가 임박한 경우 목적지 또는 대상 볼륨으로 **장애 복구**를 시작할 수 있습니다. 대상 볼륨은 활성 상태가 됩니다. 마지막으로 복제가 성공된 스냅샷이 활성화되고 마운팅을 위해 볼륨을 사용할 수 있습니다. 이전 복제 주기 이후에 소스 볼륨에 작성된 모든 데이터가 손실됩니다. 장애 복구가 시작되면 복제 관계가 뒤집힙니다. 대상 볼륨이 소스 볼륨이 되고 이전의 소스 볼륨은 **LUN 이름**(뒤에 **REP**가 표시)으로 표시되는 대상이 됩니다.

장애 복구는 [[{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}의 **스토리지**, **{{site.data.keyword.blockstorageshort}}**에서 시작합니다.

**해당 단계를 진행하기 전에 볼륨의 연결을 끊으십시오. 그렇지 않으면 결과적으로 손상되고 데이터가 유실됩니다.**

1. 활성 LUN("소스")을 클릭하십시오.
2. **복제본**을 클릭하고 **조치**를 클릭하십시오.
3. **장애 복구**를 선택하십시오.

   장애 복구가 진행 중임을 나타내는 메시지가 페이지에 표시될 것으로 예상됩니다. 또한 활성 트랜잭션이 발생 중임을 나타내는 아이콘이 **{{site.data.keyword.blockstorageshort}}**의 볼륨 옆에 표시됩니다. 아이콘 위에 마우스 커서를 두면 트랜잭션을 표시하는 창이 작성됩니다. 아이콘은 트랜잭션이 완료되면 없어집니다. 장애 복구 프로세스 중에, 구성 관련 조치는 읽기 전용입니다. 스냅샷 스케줄을 편집하거나 스냅샷 영역을 변경할 수 없습니다. 이벤트는 복제 히스토리에 로깅됩니다.<br/> 대상 볼륨이 작동 상태가 되면 다른 메시지가 수신됩니다. 원래 소스 볼륨의 LUN 이름이 업데이트되어 "REP"로 끝나고 해당 상태가 비활성이 됩니다.
   {:note}
4. **모두 보기({{site.data.keyword.blockstorageshort}})**를 클릭하십시오.
5. 활성 LUN(이전의 대상 볼륨)을 클릭하십시오.
6. 스토리지 볼륨을 호스트에 마운트하고 접속하십시오. 자세한 내용은 [여기](provisioning-block_storage.html)를 참조하십시오.


## 볼륨에서 복제본으로 장애 조치 시작

원본 소스 볼륨이 복구되면 원본 소스 볼륨으로 제어된 장애 조치를 시작할 수 있습니다. 제어된 장애 조치에서,

- 활성 소스 볼륨은 오프라인으로 설정됩니다.
- 스냅샷이 작성됩니다.
- 복제 주기가 완료됩니다.
- 조금 전에 작성된 데이터 스냅샷이 활성화됩니다.
- 소스 볼륨이 마운팅을 위해 활성화됩니다.

장애 조치가 시작되면 복제 관계가 다시 뒤집힙니다. 이제 소스 볼륨이 소스 볼륨으로 복원되고, 대상 볼륨은 다시 **LUN 이름**(뒤에 **REP**가 표시)으로 표시되는 대상 볼륨이 됩니다.

장애 조치는 [[{{site.data.keyword.slportal}} ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){:new_window}의 **스토리지**, **{{site.data.keyword.blockstorageshort}}**에서 시작합니다.

1. 활성 LUN("대상")을 클릭하십시오.
2. 오른쪽 상단에서 **복제본**을 클릭하고 **조치**를 클릭하십시오.
3. **장애 조치**를 선택하십시오.
  

   장애 복구가 진행 중임을 나타내는 메시지가 페이지에 표시될 것으로 예상됩니다. 또한 활성 트랜잭션이 발생 중임을 나타내는 아이콘이 **{{site.data.keyword.blockstorageshort}}**의 볼륨 옆에 표시됩니다. 아이콘 위에 마우스 커서를 두면 트랜잭션을 표시하는 창이 작성됩니다. 아이콘은 트랜잭션이 완료되면 없어집니다. 장애 조치 프로세스 중에, 구성 관련 조치는 읽기 전용입니다. 스냅샷 스케줄을 편집하거나 스냅샷 영역을 변경할 수 없습니다. 이벤트는 복제 히스토리에 로깅됩니다.
   {:note}
4. 오른쪽 상단에서 **{{site.data.keyword.blockstorageshort}} 모두 보기**를 클릭하십시오.
5. 활성 LUN("소스")을 클릭하십시오.
6. 스토리지 볼륨을 호스트에 마운트하고 접속하십시오. 자세한 내용은 [여기](provisioning-block_storage.html)를 참조하십시오.