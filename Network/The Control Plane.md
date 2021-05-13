## The Control Plane

## Roadmap
- [Introduction](#Introduction)
- [routing protocols](#routing-protocols)
- [The SDN control plane](#The-SDN-control-plane)

## Introduction
- data plane에서는 forwarding packets을 라우터에서 보내는 것을 생각함
- control plane에서는 routing 즉 어떻게 보낼지에 대해서 고려함
- 여기서 network control plane을 구성하는데 두가지 접근법이 있음

![one](/img/Network/Controlplane/one.png)
![one](/img/Network/Controlplane/two.png)

## routing protocols
- 좋은 path를 결정하는 것임, 여기서 좋은 path는 비용이 적고 빠르면서 혼잡도가 적은 것을 의미함
- 이를 활용하기 위해서 아래와 같이 그래프 이론을 기반으로 함

![one](/img/Network/Controlplane/three.png)
![one](/img/Network/Controlplane/four.png)

- 여기서 Routing algorithm을 구분하는 기준이 존재함
	- global
		- 모든 정보를 다 가지고 있음 라우터에서
		- link state algorithms
	- decentralized
		- 정보에 대해서 부분적으로 알고 있음
		- 그래서 반복적인 작업이 필요함
		- distance vector algorithms
	- static
		- route가 시간에 따라 느리게 바뀜
	- dynamic
		- route가 빠르게 바뀜
		- 주기적으로 업데이트하고 link cost가 바뀔때마다 반응함

- link-state algorithms 중에서 유명한 것이 Dijkstra's algorithm임

![one](/img/Network/Controlplane/five.png)
![one](/img/Network/Controlplane/six.png)
![one](/img/Network/Controlplane/seven.png)

- Dijkstra's algorithm은 n nodes일 경우 O(n^2)의 시간복잡도를 가짐
- 여기서 매우 효율적으로 만든다면 O(nlogn)까지도 가능함
- 시간과 알고리즘이 랜덤하게 되면서 반복적으로 왔다갔다 하는 문제가 발생할 수 있음

![one](/img/Network/Controlplane/eight.png)

- Distance-Vector Algorithm
- 해당 경로에서 최소 cost가 드는 path를 찾는 알고리즘, Bellman-Ford equation

![one](/img/Network/Controlplane/nine.png)
![one](/img/Network/Controlplane/ten.png)
![one](/img/Network/Controlplane/eleven.png)

- 해당 알고리즘은 시간이 지나면서 각각의 노드들이 자신의 distance vector를 이웃한 노드들고 계속 주고 받음
- 그러면서 최적값을 찾고 이를 통해 반복적으로 Bellman-Ford equation을 통해서 그 값을 갱신함

![one](/img/Network/Controlplane/twelve.png)

- 만일 여기서 link의 cost가 바뀌는 경우에 2가지 경우로 나눌 수 있음
- 첫 번째는 해당 link cost가 작아질 경우, 이 상태에서는 다시 해당 distance vector에 대해서 계산을 하면 됨, 어차피 least cost를 체킹하므로
- 하지만 link cost가 커질 경우, 이 상태에서는 바뀐것을 한 번에 알 수가 없고 여러번 반복작업을 시행해야함, 그러므로 poisoned reverse 즉 바뀐값을 무한대로 보내서 해당 경로를 바꾸게 함
- 하지만 이 경우도 절대적으로 해결하기 힘듬, link cost가 큰 값으로 많이 바뀐다면 시스템 전체를 볼 수 없으므로 모두 적용하기 힘듬

![one](/img/Network/Controlplane/thirteen.png)
![one](/img/Network/Controlplane/fourteen.png)

- link-state와 distance-vector를 비교한다면 아래와 같은 특징이 있음을 알 수 있음

![one](/img/Network/Controlplane/fifteen.png)


## The SDN control plane
- Software defined networking(SDN)
- 중앙집중형 네트워크, 전통적인 pre-router의 routing algorithm을 통한 계산이 아닌 Remote controller 즉 software를 통해서 이러한 연산을 처리함

![one](/img/Network/Controlplane/sixteen.png)

- 앞에서 본 전통적인 방식과는 다르게 software를 통해서 전체적인 상황을 보고 제어가 가능하기 때문에 매우 효율적임

![one](/img/Network/Controlplane/seventeen.png)

- 원래의 컴퓨터는 특정 용도로만 사용되는 수직적인 구조를 가지고 있었지만, Microprocessor 등장 이후 다양한 계산을 하고 개방적인 구조로 변하면서 다양한 변화가 나타남

![one](/img/Network/Controlplane/eighteen.png)

- 기존의 전통적인 routing 방식에서는 계산된 least cost path에서 직접 원하는 path로 바꾸기 위해서는 직접 link cost를 건드려서 바꿔야 했음
- 그리고 경로를 설정하는데 있어서 least cost path가 아닌 시작 router 기점으로 2개로 나뉜다고 그걸 나눠서 경로를 각각 2개로 설정하기도 힘듬

![one](/img/Network/Controlplane/nineteen.png)
![one](/img/Network/Controlplane/twenty.png)

- 그러므로 이러한 방식의 어려움을 해결하기 위해서 SDN을 활용함, 즉 SDN을 통해서 link cost, router를 직접적으로 건드리지 않는 선에서 software를 통해서 위에서 언급한 모든 부분을 제어할 수 있음
- 그래서 control plane, data plane의 방식이 명확하게 구분됨

![one](/img/Network/Controlplane/twentyone.png)
