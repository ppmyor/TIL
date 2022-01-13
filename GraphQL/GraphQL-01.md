## GraphQL로 해결할 수 있는 2가지 문제

1. Over-fetching
2. Under-fetching

#### Over-fetching

-   요청한 영역의 정보보다 많은 정보를 서버에서 받는 것
-   사용하지 않을 정보까지 받는 것은 효율x
-   GraphQL은 Over-fetching 없이 필요한 정보만 받을 수 있도록 통제 가능

#### Under-fetching

-   REST에서 하나를 완성시키기 위해 많은 소스들을 요청
-   (ex. 모든 사진의 feed 중 comment와 like 수, 알림 중에 알림을 확인했는지의 여부, 유저 프로필 중 유저명, 유저의 사진만을 필요로 하더라도 3번의 request가 필요 -> GraphQL은 원하는 정보만 받을 수 있음)

**GraphQL은 Over-fetching, Under-fetching 없이 한 query로 원하는 정보만을 받을 수 있음**
