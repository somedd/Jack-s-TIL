# 2018/07/19
## Network Programming

# 네트워크 개요
- Entity, Transmitter(Tx)-Receiver(Rx), End-Point, Terminal등의 용어들이 있지만, 컴퓨터 네트워크 용어로는 `Node - Link - Node`
- 네트워크 역사
  - 불과 50년 전을 생각해보면, 가장 유망직업은 전화교환원이었음.(PSTN으로 구성되어 있었음.)
    - PSTN: Public Swithced Telecommunications Network
  - 그 이후, 전화와 컴퓨터가 복잡해지면서, 컴퓨터가 하나의 노드를 담당하고, 전세계를 묶어주는 Link가 구성이되었음.
  - 요새는, IMS(All-IP). 모든 통신이 데이터를 통해 이루어진다. 또한, 모든 장비들이 다 프로그램이다.
    - 하지만, 이와 같이 통신을 하려면 규칙이 필요하다. 이를 정하는 기관이 IETF. 표준안을 정한다.
  - 네트워크 프로그래밍을 한다는 것은
    1. 각 용어를 이해하였는가
    2. 위 용어들의 컨셉을 알고 있는 상태에서 활용할 줄 아는가.

# OSI(Open Stystem Interconnection) 7 Layer (외우지 말고, 이해를 하면 된다.)
- Upper Layers
  - 7.Application Layer: 메일형식으로 주고 받을 것이닞? 다른 Format으로 주고 받을 지를 결정한다.
  - 6.Presentation Layer: 어떤 식으로 표현할 것인가?(HTTP? Text? 영어로? 한글로? 를 결정.)
  - 5.Session Layer: 내가 누군지 밝히고, 확인을 담당.

- Transport Service: 전화기를 산다고 했을 때까지의 단계라고 생각하면 된다.
  - 4.Transport Layer: PORT가 할당이 된다. (Socket이 생김.) 어떻게 주고받을 것인지?(TCP? UDP?)
  - 3.Network Layer: IP가 결정된다.(공유기에 연결하는 것.)
  - 2.Data Link layer: LAN카드를 설정하는 것.
  - 1.Physical Layer: Lan카드 자체.

- Mac의 Network Tools에서 각종 동작들 확인.

# Socket
- 각 정해진 PORT들이 할당되려면, 소켓을 만들어야 한다.
- 소켓을 정할 때, Client or Server인지를 정해야 한다.
  - Clent는 Connect
  - Server는 Listen
- TCP vs UDP
  - UDP는 순서가 보장이 안되고, 실패도 보장이 안된다. 그렇기 때문에, 순서랑 상관없이 보내는 경우에 쓴다.
  - TCP는 순서가 보장이 되어야하고, 실패가 보장이 되어야할 때 사용. 확인을 받아야 하는 경우.
  - 프로토콜마다 TCP기반인 것도 있고, UDP 기반인 것도 있다.
- 모든 네트워크 프로그래밍은 소켓이다. 하지만, 우리가 소켓을 안만들어도 되는 이유는 추상화된 라이브러리가 있기 때문이다.

# iOS Networking
- iOS에서의 계층
  - Application
  - Foundation : 대부분은 이를 사용하도록 권장한다.
    - 이 중에 NSURLConnection을 사용했고, 권장 또한 많이 했다. 사파리를 만들 때 사용되었던 것이지만, 현재는 Deprecated됐다. Background로 들어가도 기기 내부에 저장하거나, 서버에 올리는 기능이 생긴 것임.
    - 이유는 App이 Background로 들어가면 동작이 안되는 것이 문제.
      - 그 후, NSURLSession으로 바뀌었다. 방금 문제를 보완하기 위해. Background로 들어가도 기기 내부에 저장하거나, 서버에 올리는 기능이 생긴 것임.
      - 향 후, Network APIs가 생긴다. NSURLSession 말고 조금 더 Low단에 접근이 필요한 경우 사용하도록 생긴다. iOS 12부터 가능하다.
  - CFNetwork : 현재 사용가능하지만, 실제로 쓰지 않는다.
  - Core OS (Darwin) : 현재 사용가능하지만, 쓰기 어려워서 잘 사용하지 않음.

- 고려해야할 요소
  - Security
  - Packet Problems
  - Bandwidth
  - Latency
  - Service Discovery
  - Asymmetric Connectivity
  - Mobility

# NSURLSession
- Configuration
  - NSURLSessionConfiguration object
  - Properties that affect transfers TLS levels
    - Cellular usage
    - Network service type
    - Cookie policies
    - Cache policies
    - Storage objects
    - Request & resource timeouts

- Sesseion
  - Singleton shared session:  델리게이트 없이 간단한 비동기 요청
  - Default session: 기본 설정 세션. 커스텀 설정 가능
  - Ephemeral session: 델리게이트 없이 비공개(private) 세션
  - Background session: 백그라운드 동작을 위한 세션

- Task
  - dataTask: Get명령처럼 서버에 있는 것을 받아오는 Task
  - uploadTask: 말 그대로 서버에 업로드 하는 Task
  - downloadTask: 해당 파일을 다운로드해서 저장하는 Task.
  - 중요한 것은 해당 Task가 끝나서 응답을 받을 때까지는 해당 Task가 살아있어야 한다.

- HTTP 규격은 생각보다 간단하다. 모두 Text로 되어있고, \n에 따라 구분이 되며, \n이 두 번 일 경우, Header와 Body가 구분이 된다.
- NSURLSession은 비동기 처리인데, 동기방식으로 처리하고자 할 떄,
  ```
  let data = Data(contentsOf: URL(String: "address"))
  ```

# Network.framework (iOS 12
- Connection Setup
  ```
  // Create an outbound connection
  import Network
  let connection = NWConnection(host: "mail.example.com", port: .imaps, using: .tls)
  connection.stateUpdateHandler = { (newState) in
  switch(newState) {
  case .ready:
  // Handle connection established
  case .waiting(let error):
  // Handle connection waiting for network
  case .failed(let error):
  // Handle fatal connection error
  default: break
  }
  }
  connection.start(queue: myQueue)
  ```

- Listener
  ```
  // UDP Bonjour listener
   do {
   if let listener = try NWListener(parameters: .udp) {
   // Advertise a Bonjour service
   listener.service = NWListener.Service(type: “_camera._udp”)
    }
  listener.newConnectionHandler = { (newConnection) in
   // Handle inbound connections
   newConnection.start(queue: myQueue)
   }
   listener.start(queue: myQueue)
   }
   } catch {
     // Handle listener creation error
   }
   //
  ```

- Send
  ```
  // Send a single frame
  func sendFrame(_ connection: NWConnection, frame: Data) {
  // The .contentProcessed completion provides sender-side back-pressure
  connection.send(content: frame, completion: .contentProcessed { (sendError) in
  if let sendError = sendError {
  // Handle error in sending
  } else {
  // Send has been processed, send the next frame
  let nextFrame = generateNextFrame()
  }
  sendFrame(connection, frame: nextFrame)
  })
  }
  ```

- Receive
  ```
  // Read one header from the connection
  func readHeader(connection: NWConnection) {
  // Read exactly the length of the header
  let headerLength: Int = 10
  connection.receive(minimumIncompleteLength: headerLength, maximumLength: headerLength)
  { (content, contentContext, isComplete, error) in
  if let error = error {
  // Handle error in reading
   } else {
   // Parse out body length
   readBody(connection, bodyLength: bodyLength)
   }
  }
  }
     // Follow the same pattern as readHeader() to read exactly the body length
   func readBody(_ connection: NWConnection, bodyLength: Int) { ... }
  ```
