## The Control Plane

## Roadmap
- [Introduction](#Introduction)
- [routing protocols](#routing-protocols)

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

