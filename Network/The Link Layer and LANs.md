## The Link Layer and LANs

## Roadmap
- [Introduction](#Introduction)



## Introduction
- Link layer에서는 hosts와 routers에 대해서 링크로 연결되는 것들로 nodes라고 부름
- 이러한 인접한 노드들을 연결하여서 데이터들이 점대점으로 전송될 수 있도록 links로 연결함
- 이러한 데이터를 캡슐화하여서 frame으로 만들어서 전송하고 보냄
- 한 번 이런식의 데이터가 주고 받을 때 점대점 방식으로 매우 많이 전송이 오고 가게됨
- 그리고 아래와 같은 특징을 지님

![one](/img/Network/Linklayer/one.png)

- 이러한 link layer는 모든 host들에 적용이 되는데 여기서 이 host에 적용될 때 아래와 같이 물리적인 hardware를 매개하여서 사용이 됨
- 여전히 이러한 부분의 칩셋은 존재를 함
- 그 중 대표적인 것이 adaptor인데 아래와 같이 datagram을 보내는데 있어서 전송과 수신 그리고 이를 캡슐화해서 보내는데 역할을 함

![one](/img/Network/Linklayer/two.png)
![one](/img/Network/Linklayer/three.png)
