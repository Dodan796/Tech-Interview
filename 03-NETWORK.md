## 네트워크

<details>
  <summary><h3>1. 쿠키와 세션의 차이에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 세션 방식의 로그인 과정에 대해 설명해 주세요.</li>
<li> HTTP의 특성인 Stateless에 대해 설명해 주세요.</li>
<li> Stateless의 의미를 살펴보면, 세션은 적절하지 않은 인증 방법 아닌가요?</li>
<li> 규모가 커져 서버가 여러 개가 된다면, 세션을 어떻게 관리할 수 있을까요?</li>
</ul>
</details>

<details>
  <summary><h3>2. HTTP 응답코드에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 401 (Unauthorized) 와 403 (Forbidden)은 의미적으로 어떤 차이가 있나요?</li>
<li> 200 (ok) 와 201 (created) 의 차이에 대해 설명해 주세요.</li>
<li> 필요하다면 저희가 직접 응답코드를 정의해서 사용할 수 있을까요? 예를 들어 285번 처럼요. </li>
</ul>
</details>

<details>
  <summary><h3>3. HTTP Method 에 대해 설명해 주세요.</h3></summary>
  HTTP는 클라이언트와 서버 간의 통신에서 동작을 명시하기 위해 다양한 메서드를 제공합니다. 
  가장 대표적인 메서드로는 GET, POST, PUT, PATCH, DELETE 등이 있습니다.
  GET은 리소스를 조회할 때 사용되며, 요청 본문을 가지지 않습니다.

  POST는 리소스를 생성하거나 서버에 데이터를 전송할 때 사용됩니다.

  PUT은 전체 리소스를 대체할 때 사용되며,

  PATCH는 리소스의 일부를 수정할 때 사용됩니다.

  DELETE는 리소스를 삭제하는 데 사용됩니다.
<ul>
<li> HTTP Method의 멱등성에 대해 설명해 주세요.</li>
  HTTP 메서드의 멱등성(Idempotency)이란, 동일한 요청을 여러 번 보내더라도 서버의 상태가 처음 요청과 이후 요청에서 변하지 않는 특성을 의미합니다.
예를 들어 GET, PUT, DELETE는 멱등한 메서드이며, 같은 요청을 여러 번 보내더라도 서버 자원의 상태가 같게 유지됩니다.
반면 POST는 멱등하지 않은 메서드로, 동일한 요청을 여러 번 전송하면 데이터가 중복 생성될 수 있습니다.
이러한 멱등성 개념은 네트워크 장애나 재요청 상황에서 안전한 재시도를 가능하게 하므로, REST API 설계 시 중요한 고려 요소입니다.
<li> GET과 POST의 차이는 무엇인가요?</li>
  GET은 주로 리소스의 조회에 사용되며, 요청 파라미터를 URL의 쿼리 문자열로 전달하기 때문에 캐싱, 즐겨찾기, 브라우저 히스토리 등의 기능과 호환됩니다. 
  하지만 데이터 길이에 제한이 있고 민감한 정보를 포함하기에는 적절하지 않습니다.
  POST는 데이터를 요청 본문(body)에 담아 전송하기 때문에 대용량 데이터 전송이나 민감한 정보 제출에 적합하며, 서버에 리소스를 생성하거나 상태를 변경할 때 주로 사용됩니다. 
  따라서 REST API 설계에서도 의미론적으로 분리되어 사용됩니다.
  
<li> POST와 PUT, PATCH의 차이는 무엇인가요?</li>
POST는 주로 새로운 리소스를 생성하거나, 서버에서 정의된 로직에 따라 데이터를 처리할 때 사용됩니다. 멱등하지 않기 때문에 같은 요청을 반복하면 결과가 달라질 수 있습니다.

PUT은 대상 리소스를 전체 대체하는 데 사용되며, 지정된 URI가 없으면 새로 생성될 수도 있습니다. 멱등성이 보장되므로 반복 요청해도 결과는 동일합니다.

PATCH는 리소스의 일부 필드만 수정할 때 사용되며, 상대적으로 적은 데이터만 전송하므로 효율적입니다. PATCH는 엄격한 멱등성을 요구하지 않지만, 실무에서는 가능하면 멱등하게 구현하는 경우도 많습니다.
<li> HTTP 1.1 이후로, GET에도 Body에 데이터를 실을 수 있게 되었습니다. 그럼에도 불구하고 왜 아직도 이런 방식을 지양하는 것일까요?</li>
HTTP/1.1 스펙상으로는 GET 요청에서도 요청 본문을 전송하는 것이 가능하지만, 실무에서는 여전히 이를 지양합니다.
그 이유는 두 가지입니다.
첫째, HTTP 표준이 GET 요청의 본문에 대해 명확한 의미를 정의하지 않기 때문에, 다양한 프록시 서버, 캐시 서버, 웹 서버, 클라이언트 라이브러리들이 이를 일관되게 처리하지 못할 수 있습니다.
둘째, GET은 본래 조회 목적으로 사용되며, 쿼리 파라미터를 통해 충분히 요청 정보를 전달할 수 있으므로, 본문을 사용할 필요성이 낮습니다.
결과적으로 호환성과 예측 가능한 동작을 유지하기 위해, GET 요청에서 Body 사용은 권장되지 않습니다.
</ul>
</details>

<details>
  <summary><h3>4. HTTP에 대해 설명해 주세요.</h3></summary>
  HTTP(Hypertext Transfer Protocol)는 웹 상에서 클라이언트와 서버가 데이터를 주고받기 위한 애플리케이션 계층 프로토콜입니다.
비연결성(Connectionless)과 비상태성(Stateless)을 특징으로 하며, 요청(Request)과 응답(Response) 형태로 동작합니다.
HTTP/1.1부터는 Persistent Connection을 통해 커넥션 재사용이 가능해졌으며, 이후 HTTP/2는 멀티플렉싱과 헤더 압축을 도입하여 성능을 대폭 개선했습니다.
현재는 HTTP/3까지 발전했으며, 전송 계층에 QUIC 프로토콜을 사용해 지연 시간을 줄이고 보안을 강화했습니다.
<ul>
<li> 공개키와 대칭키에 대해 설명해 주세요.</li>
  암호화에는 두 가지 주요 방식이 있으며, 대칭키 암호화는 동일한 키로 데이터를 암호화하고 복호화하는 방식입니다. 속도가 빠르고 간단하지만, 키의 안전한 공유가 어렵다는 단점이 있습니다.
반면 공개키 암호화는 서로 다른 키를 사용하는 방식으로, 공개키로 암호화한 데이터는 개인키로만 복호화할 수 있습니다. 이를 통해 키 교환 과정에서의 보안성을 확보할 수 있으며, HTTPS의 SSL/TLS 통신에서도 이러한 방식이 활용됩니다.


<li> 왜 HTTPS Handshake 과정에서는 인증서를 사용하는 것 일까요?</li>
HTTPS에서 인증서는 서버가 신뢰할 수 있는 주체임을 증명하기 위한 수단입니다.
클라이언트가 서버와 통신을 시작할 때, 서버는 인증서를 제공하며, 이는 공인된 인증 기관(CA)이 발급한 것이어야 합니다.
클라이언트는 이 인증서를 검증한 후, 서버의 공개키를 신뢰하고 대칭키를 암호화하여 전송합니다.
이 과정을 통해 중간자 공격(MITM)을 방지하고, 통신 상대의 신원을 검증할 수 있어 안전한 연결이 보장됩니다.
<li> SSL과 TLS의 차이는 무엇인가요?</li>
SSL(Secure Sockets Layer)은 넷스케이프가 개발한 보안 프로토콜로, HTTPS의 초기 버전에서 사용되었습니다. 하지만 보안 취약점으로 인해 SSL 2.0과 3.0은 이미 사용이 중지되었습니다.
현재는 **TLS(Transport Layer Security)**가 그 후속 프로토콜로, SSL보다 더 안전한 암호화 알고리즘과 인증 메커니즘을 제공합니다.
즉, TLS는 SSL의 발전형이며, 오늘날 우리가 말하는 "HTTPS 보안 연결"은 실제로 TLS 기반으로 동작합니다.

</ul>
</details>

<details>
  <summary><h3>5. 웹소켓과 소켓 통신의 차이에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 소켓과 포트의 차이가 무엇인가요?</li>
<li> 여러 소켓이 있다고 할 때, 그 소켓의 포트 번호는 모두 다른가요?</li>
<li> 사용자의 요청이 무수히 많아지면, 소켓도 무수히 생성되나요?</li>
</ul>
</details>

<details>
  <summary><h3>6. HTTP/1.1과 HTTP/2의 차이점은 무엇인가요?</h3></summary>
<ul>
<li> HOL Blocking 에 대해 설명해 주세요.</li>
<li> HTTP/3.0의 주요 특징에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>7. TCP와 UDP의 차이에 대해 설명해 주세요.</h3></summary>
<ul>
<li> Checksum이 무엇인가요?</li>
<li> TCP와 UDP 중 어느 프로토콜이 Checksum을 수행할까요?</li>
<li> 그렇다면, Checksum을 통해 오류를 정정할 수 있나요? </li>
<li> TCP가 신뢰성을 보장하는 방법에 대해 설명해 주세요.</li>
<li> TCP의 혼잡 제어 처리 방법에 대해 설명해 주세요.</li>
<li> 왜 HTTP는 TCP를 사용하나요?</li>
<li> 그렇다면, 왜 HTTP/3 에서는 UDP를 사용하나요? 위에서 언급한 UDP의 문제가 해결되었나요?</li>
<li> 그런데, 브라우저는 어떤 서버가 TCP를 쓰는지 UDP를 쓰는지 어떻게 알 수 있나요?</li>
<li> 본인이 새로운 통신 프로토콜을 TCP나 UDP를 사용해서 구현한다고 하면, 어떤 기준으로 프로토콜을 선택하시겠어요?</li>
</ul>
</details>

<details>
  <summary><h3>8. DHCP가 무엇인지 설명해 주세요.</h3></summary>
<ul>
<li> DHCP는 몇 계층 프로토콜인가요? </li>
<li> DHCP는 어떻게 동작하나요?</li>
<li> DHCP에서 UDP를 사용하는 이유가 무엇인가요?</li>
<li> DHCP에서, IP 주소 말고 추가로 제공해주는 정보가 있나요?</li>
<li> DHCP의 유효기간은 얼마나 긴가요?</li>
</ul>
</details>

<details>
  <summary><h3>9. IP 주소는 무엇이며, 어떤 기능을 하고 있나요?</h3></summary>
<ul>
<li> IPv6는 IPv4의 주소 고갈 문제를 해결하기 위해 만들어졌지만, 아직도 수많은 기기가 IPv4를 사용하고 있습니다. 고갈 문제를 어떻게 해결할 수 있을까요?</li>
<li> IPv4와 IPv6의 차이에 대해 설명해 주세요.</li>
<li> 수많은 사람들이 유동 IP를 사용하고 있지만, 수많은 공유기에서는 고정 주소를 제공하는 기능이 이미 존재합니다. 어떻게 가능한 걸까요?</li>
<li> IPv4를 사용하는 장비와 IPv6를 사용하는 같은 네트워크 내에서 통신이 가능한가요? 가능하다면 어떤 방법을 사용하나요? </li>
<li> IP가 송신자와 수신자를 정확하게 전송되는 것을 보장해 주나요?</li>
<li> IPv4에서 수행하는 Checksum과 TCP에서 수행하는 Checksum은 어떤 차이가 있나요?</li>
<li> TTL(Hop Limit)이란 무엇인가요? </li>
<li> IP 주소와 MAC 주소의 차이에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>10. OSI 7계층에 대해 설명해 주세요.</h3></summary>
<ul>
<li> Transport Layer와, Network Layer의 차이에 대해 설명해 주세요.</li>
<li> L3 Switch와 Router의 차이에 대해 설명해 주세요.</li>
<li> 각 Layer는 패킷을 어떻게 명칭하나요? 예를 들어, Transport Layer의 경우 Segment라 부릅니다.</li>
<li> 각각의 Header의 Packing Order에 대해 설명해 주세요.</li>
<li> ARP에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>11. 3-Way Handshake에 대해 설명해 주세요.</h3></summary>
<ul>
<li> ACK, SYN 같은 정보는 어떻게 전달하는 것 일까요?</li>
<li> 2-Way Handshaking 를 하지않는 이유에 대해 설명해 주세요.</li>
<li> 두 호스트가 동시에 연결을 시도하면, 연결이 가능한가요? 가능하다면 어떻게 통신 연결을 수행하나요?</li>
<li> SYN Flooding 에 대해 설명해 주세요.</li>
<li> 위 질문과 모순될 수 있지만, 3-Way Handshake의 속도 문제 때문에 이동 수를 줄이는 0-RTT 기법을 많이 적용하고 있습니다. 어떤 방식으로 가능한 걸까요?</li>
</ul>
</details>

<details>
  <summary><h3>12. 4-Way Handshake에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 패킷이 4-way handshake 목적인지 어떻게 파악할 수 있을까요?</li>
<li> 빨리 끊어야 할 경우엔, (즉, 4-way Handshake를 할 여유가 없다면) 어떻게 종료할 수 있을까요?</li>
<li> 4-Way Handshake 과정에서 중간에 한쪽 네트워크가 강제로 종료된다면, 반대쪽은 이를 어떻게 인식할 수 있을까요?</li>
<li> 왜 종료 후에 바로 끝나지 않고, TIME_WAIT 상태로 대기하는 것 일까요? </li>
</ul>
</details>

<details>
  <summary><h3>13. www.github.com을 브라우저에 입력하고 엔터를 쳤을 때, 네트워크 상 어떤 일이 일어나는지 최대한 자세하게 설명해 주세요.</h3></summary>
<ul>
<li> DNS 쿼리를 통해 얻어진 IP는 어디를 가리키고 있나요?</li>
<li> Web Server와 Web Application Server의 차이에 대해 설명해 주세요. </li>
<li> URL, URI, URN은 어떤 차이가 있나요? </li>
</ul>
</details>

<details>
  <summary><h3>14. DNS에 대해 설명해 주세요.</h3></summary>
<ul>
<li> DNS는 몇 계층 프로토콜인가요? </li>
<li> UDP와 TCP 중 어떤 것을 사용하나요?</li>
<li> DNS Recursive Query, Iterative Query가 무엇인가요?</li>
<li> DNS 쿼리 과정에서 손실이 발생한다면, 어떻게 처리하나요?</li>
<li> 캐싱된 DNS 쿼리가 잘못 될 수도 있습니다. 이 경우, 어떻게 에러를 보정할 수 있나요?</li>
<li> DNS 레코드 타입 중 A, CNAME, AAAA의 차이에 대해서 설명해주세요.</li>
<li> hosts 파일은 어떤 역할을 하나요? DNS와 비교하였을 때 어떤 것이 우선순위가 더 높나요?</li>
</ul>
</details>

<details>
  <summary><h3>15. SOP 정책에 대해 설명해 주세요.</h3></summary>
<ul>
<li> CORS 정책이 무엇인가요?</li>
<li> Preflight에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>16. Stateless와 Connectionless에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 왜 HTTP는 Stateless 구조를 채택하고 있을까요?</li>
<li> Connectionless의 논리대로면 성능이 되게 좋지 않을 것으로 보이는데, 해결 방법이 있을까요?</li>
<li> TCP의 keep-alive와 HTTP의 keep-alive의 차이는 무엇인가요?</li>
</ul>
</details>

<details>
  <summary><h3>17. 라우터 내의 포워딩 과정에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 라우팅과 포워딩의 차이는 무엇인가요?</li>
<li> 라우팅 알고리즘에 대해 설명해 주세요.</li>
<li> 포워딩 테이블의 구조에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>18. 로드밸런서가 무엇인가요?</h3></summary>
<ul>
<li> L4 로드밸런서와, L7 로드밸런서의 차이에 대해 설명해 주세요.</li>
<li> 로드밸런서 알고리즘에 대해 설명해 주세요.</li>
<li> 로드밸런싱 대상이 되는 장치중 일부 장치가 문제가 생겨 접속이 불가능하다고 가정해 봅시다. 이 경우, 로드밸런서가 해당 장비로 요청을 보내지 않도록 하려면 어떻게 해야 할까요?</li>
<li> 로드밸런서 장치를 사용하지 않고, DNS를 활용해서 유사하게 로드밸런싱을 하는 방법에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>19. 서브넷 마스크와, 게이트웨이에 대해 설명해 주세요.</h3></summary>
<ul>
<li> NAT에 대해 설명해 주세요. </li>
<li> 서브넷 마스크의 표현 방식에 대해 설명해 주세요.</li>
<li> 그렇다면, 255.0.255.0 같은 꼴의 서브넷 마스크도 가능한가요?</li>
</ul>
</details>

<details>
  <summary><h3>20. 멀티플렉싱과 디멀티플렉싱에 대해 설명해 주세요.</h3></summary>
<ul>
<li> 디멀티플렉싱의 과정에 대해 설명해 주세요.</li>
</ul>
</details>

<details>
  <summary><h3>21. XSS에 대해서 설명해 주세요.</h3></summary>
<ul>
<li> CSRF랑 XSS는 어떤 차이가 있나요?</li>
<li> XSS는 프론트엔드에서만 막을 수 있나요?</li>
</ul>
</details>
