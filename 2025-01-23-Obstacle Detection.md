# 장애물 회피



## Basic Algorithm of Autonomous Driving

![image-20250120162036906](../images/2025-01-23-Obstacle Detection/image-20250120162036906.png)

> 라이다를 이용한 장애물 검출 및 자동차 경로계획에 관한 연구.pdf
>
> [Figure 1.][1]



장애물 회피를 위해서 크게 Obstacle Detection과  Navigation을 나눌 수 있으며 

Obstacle Detection에서는 Clustrering - Obstacle detection - Calculating obstacle distance으로 나눌 수 있다.

Navigation System에서는 Global Path Planning / Local Path Planning 으로 나눌 수 있다.

---



## Obstacle Detection

  Obstacle Detection시 장애물과 지면이 붙어있을 경우 하나의 객체로 묶인다. 이 경우 장애물의 수를 정확히 파악하기 어렵기 때문에 군집화의 전처리 과정이 필요하다. 더불어, 오르막길이나 먼 거리의 도로의 검출을 고려해 z축으로 0.5 [m] 이하 범위에 해당하는 Point Cloud는 지면으로 간주하여 제거한다. 

> 라이다를 이용한 장애물 검출 및 자동차 경로계획에 관한 연구.pdf
>
> [Figure 2.][1]
>
> [][1]



### Clustering

---



####  - K-means Clustering 

  주어진 데이터를 k개로 묶는 알고리듬. 각 객체의 분산을 최소화 하도록 함.

  i번째 객체의 중심 $\mu_i$, 객체에 속하는 점의 집합 $S_i$, 전체분산 $V$의 식은 다음과 같다.
$$
V = \sum_{i=1}^k \sum_{j \in S_i} |x_j - \mu_i|^2
$$

> 원래 분산의 의미를 생각하면 저 식에는 오류가 있다. 정확한 분산에 대한 표현은 아니다.
>
> 분산이란, 관측값에서 평균을 뺀 값을 제곱하고, 그것을 모두 더한 후 전체 개수로 나눠서 구하는 것이다.
>
> 하지만 전체 개수로 나누는 항이 빠졌고 이를 표현한 제대로 된 분산식은 다음과 같다.
> $$
> V_{\text{평균}} = \frac{1}{k} \sum_{i=1}^k \frac{1}{|S_i|} \sum_{j \in S_i} |x_j - \mu_i|^2
> $$
>   $S_i$에 대한 항이 빠질 수 있던 이유는 어쨌든 중심값과의 거리가 가장 짧은 분산이 필요한 것이기 때문에 $k, S_i$ 두 항은 하나의 곱셈상수로 표현할 수 있다.
>
> 즉, 이는 $V$를 최소화 하는 $S_i$를 찾는 것이 목적이기 때문에 곱셈상수는 필요 없는 것이다.



![](../images/2025-01-23-Obstacle Detection/K_means_clustering_algorythm-1737643975795.png)

> K-means Clustering Flow Chart







#### - K-Medians Clustering

#### - Mean-Shift Clustering

> https://saint-swithins-day.tistory.com/81

#### - DBSCAN

#### - Gaussian Mixture Models (GMM) 을 사용한 Expectation-Macimization (EM) Clustering

> ![image-20250122173922973](C:\Users\GihyunPark\AppData\Roaming\Typora\typora-user-images\image-20250122173922973.png)

#### - Agglomerative Hierarchical Clustering

> http://www.nextobe.com/2020/05/14/%EB%8D%B0%EC%9D%B4%ED%84%B0-%EA%B3%BC%ED%95%99%EC%9E%90%EA%B0%80-%EC%95%8C%EC%95%84%EC%95%BC-%ED%95%A0-5%EA%B0%80%EC%A7%80-%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0%EB%A7%81-%EC%95%8C%EA%B3%A0%EB%A6%AC/

> https://daebaq27.tistory.com/49



## Reference

[1]: file:///E:/0%20undergraduate/HADA/Mission/Obstacle%20Detection/paper/%5BObstacle%20Path%20Planning%5D%20Research%20on%20obstacle%20detection%20and%20vehicle%20path%20planning%20using%20lidar.pdf