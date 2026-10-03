VPC
= "사설 네트워크" -> "내가 사용할 모든 네트워크를 할당 받은것"

Subnet
= "실제 내가 사용할 네트워크" -> "VPC로부터 분할해서 사용함"
    public : 외부 인터넷과 연결이 가능한 서브넷으로 사용 (예컨데 web)
    private : 외부 인터넷 연결이 불가능한 서브넷으로 사용 (예컨데 db)

Route Table
= "서버들 관리하는 주소록같은 것"
    public : public subnet에서 사용할 목적으로 만든 public rt
            : IG + local
    private : private subnet에서 사용할 목적으로 만든 private rt
            : local

Internet Gateway(IG)
= "인터넷으로 향하는 통로 역할의 게이트웨이"
    public에 여길 등록해놔야 인터넷으로 갈 수 있음. 사실상 public인 이유.


Security Group
= "인터페이스에 부여하는 일종의 보안 정책들"
= HTTP, HTTPS, SSH만 인바운드 트래픽 허용시키는게 Web서버. 아웃바운드는 다 차단.
= Stateful

EC2
= 인스턴스 객채.
= HTTP, HTTPS 다운했음.
= 호스트에서 웹브라우저로 SSH, HTTP, HTTPS 접속 성공



