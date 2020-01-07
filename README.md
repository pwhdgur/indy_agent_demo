# indy_agent_demo

< 하이퍼 렛저 인디 에이전트 데모 >
참고 사이트 : https://github.com/hyperledger/education/tree/master/LFS171x/indy-material/nodejs

- 유용한 데모으로 유용하나 개발 및 상용화하기 위해서는 아래 사이트부터 시작하십시요.
https://github.com/hyperledger/aries-cloudagent-python/tree/master/docs/GettingStartedAriesDev 

1. 전제 조건 (Dependencies)
- Docker, including Docker Compose installed
- git installed

In Browser
$ git clone https://github.com/hyperledger/education
$ cd education/LFS171x/indy-material/nodejs

2. Starting the Demonstration
$ cd education/LFS171x/indy-material/nodejs

2.1 Run the command
$ ./manage build
$ ./manage up

2.2 로그 확인
$ ./manage logs

3. Demo Web Site
Alice : http://localhost:3000
Faber College : http://localhost:3002
Acme Corporation : http://localhost:3003
Blockchain Ledger Explorer : http://localhost:9000
Bob : http://localhost:3001
Thrift Bank : http://localhost:3004

4. Demo Scenario
4.1 Step 1
- 각각의 사이트의 관계(Relationships)나 메시지(Messages)가 없습니다.
- 각각의 사이트는 정부로부터 하나의 자격 증명을 가지고 있으며, 신원의 공식 "이름"(Alice, Faber 등)을 가지고 있습니다.
- 각각의 사이트는 Proof Requests와 Issuing(증명 요청 및 발급)에는 몇 가지 사항이 있습니다. 나중에 살펴 보겠습니다.
- 화면 하단에 각 사용자의 DID Endpoint가 있음을 알 수 있습니다. 이를 이용해 Agent를 연결하여 메시지를 교환할 수 있습니다.

4.2 Step 2 : Faber 설정
- Faber Agent 탭으로 이동하여 Issuing을 클릭
- Submit 버튼을 클릭
- Credential Definition 창에서 Schema(Transcript 1.3)를 선택하고, 태그를 지정한 후 Submit 버튼을 클릭
(Credential Difinition을 생성하는 프로세스는 Credential Definition이 안전하고 Faber만 사용할 수 있도록 Indy가 암호화 키를 생성하므로 약간의 시간이 소요됩니다.)

4.3 Step 3: 관계 형성(Establishing Relationships)
Alice가 Faber College에서 성적 증명서를 받으려면 Alice는 Faber와 디지털 관계를 맺어야 합니다. 
Alice는 Faber용 Endpoint DID를 사용하여 연결 요청을 전송해 이를 수행.

- Alice Agent 탭에서 Send New Connection Request 버튼을 클릭
- Faber Agent 탭에서 Faber의 Endpoint DID를 복사해 Alice Agent 탭에서 "Send Connection Request" 팝업창에 붙여넣고 Send Connection Request 버튼을 클릭
- Messages 메뉴를 클릭한 후, Accept 버튼을 클릭 (Alice & Faber Agent)

4.4 Step 4: 자격증명에 관한 모든 것(It's All About Your Credentials)
Alice는 Acme에 일자리를 지원하려면 성적증명서가 필요함 (Alice와 Faber는 관계를 맺고 있으므로 계속해서 성적증명서를 요청할수 있음)

- Faber 브라우저 탭으로 이동하여 Issuing 메뉴 항목을 클릭
- Send Credential Offer 창에서 관계(Alice)를 선택한 후 Credential Definition(MyTranscript)를 선택하고 Submit을 클릭
- Alice 브라우저 탭으로 돌아가면 Message에 Faber로부터 새로운 Credential 요청이 온 것을 확인할 수 있습니다. Accept 버튼을 클릭
- Credentials 메뉴를 클릭 

Alice는 이제 Government ID와 성적증명서(Transcript) 두 가지 Credential을 갖습니다
 
4.5 Step 5: 구직 신청(Applying for the Job)

4.5.1 Alice와 Acme 관계설정
Alice는 Faber로부터 자신의 성적증명서를 받았습니다. 이제 그녀가 해야할 일은 직업을 갖는 것입니다!
Acme와 인터뷰를 했고 성적증명서를 제출하는일만 남았습니다.
Alice는 먼저 Acme와 관계를 맺어야 합니다.

- Send New Connection Request를 클릭
- Acme의 Endpoint DID를 복사해서 붙여넣고 Send Connection Request 버튼을 클릭
- Messages 메뉴를 클릭한 후, Accept 버튼을 클릭

4.5.2 Acme이 Alice의 성적증명서를 Faber에 요청하기위한 흐름.
Acme 브라우저 탭에서 실행:
- Proof Requests 메뉴 클릭
- Relationship: Alice 선택
- Select a Proof Request: Other (Paste Proof Request Here) --> 선택
- Faber 탭에서 복사한 텍스트 붙여넣기 (현재 데모 시나리오에서는 해킹해서 서비스 흐름을 설명하는데 목적이 있음)
  1. Faber 브라우저 탭
  2. Proof Requests 메뉴를 클릭
  3. Proof Request 선택 드롭다운에서 "Transcript-Data"를 선택
  4. 오른쪽 상자의 텍스트(JSON 구조)는 "name": "Transcript-Data"로 시작하는 내용을 All-Copy
- Submit 버튼 클릭

Alice 브라우저 탭으로 돌아가서 Messages 메뉴를 클릭하십시오. Alice는 Proof에 대한 성적증명서 속성("claims")을 제공하는 것에 동의합니다.
Alice는 다음과 같은 내용을 증명하기 위해 Transcript-Data의 유효성을 검사.
- Faber College의 claims
- Alice에 의해 제공된 claims
- 무단으로 변경되지 않은 claims


< 프로젝트 설치 >
cd /opt/gopath/src/github.com/hyperledger
git clone https://github.com/hyperledger/education/
cd education/LFS171x/indy-material/nodejs

< 빌드 >
./manage build

< 실행 >
./manage up

< 로그 확인 >
./manage logs

< 중지 >
./manage down

$ docker rm $(docker ps -aq)

$ docker rmi $(docker images dev-* -q)

$ docker network prune
