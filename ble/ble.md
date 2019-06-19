https://medium.com/@zoyi_product/bluetooth-low-energy-ble-84b03705ffca

BLE (Bluetooth Low Energy)

How they communicate?

Advertise(= Broadcast) vs Connection

Advertise perspective role
- Advertiser(= Broadcaster) : Send Non-Connectable Advertising Packet periodically.
- Observer : Scan Non-Connectable Advertising Packet from Advertiser periodically.

Connection perspective role
- Central(= Master) : Scan Connectable Advertising Packet from Peripheral periodically.
- Peripheral(= Slave) : Send Connectable Advertising Packet periodically.


Bluetooth Protocol Stack, Packet Type

    Physical Layer
- 2.4GHz band, 40 channels
- 3 channels for Advertising Channel, 37 channels for Data Channel

    Link Layer
                   Connection
Advertiser, Scanner  ----->  Slave, Master

Scanner Scanning Mode
- Passive Scanning : Receive Advertising Packet, No Response
- Active Scanning : Receive Advertising Packet, Scan Request(Scanner) -> Scan Response(Advertiser)

    GAP (Generic Access Profile)
                     Connection
Broadcaster, Observer  ----->  Peripheral, Central

    GATT (Generic Attribute Profile)
- Client : Server에 Data를 요청한다. 하지만 처음에는 Server에 대해서 아는 것이 없기 때문에, Service Discovery라는 것을 수행한다. 이 후, Server에서 전송된 Response, Indication, Notification을 수신할 수 있다.
- Server : Client에게 Request를 받으면 Response를 보낸다. 또한 Client가 사용할 수 있는 User Data를 생성하고 저장해놓는 역할을 한다.
