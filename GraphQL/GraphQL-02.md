## schema

-   받거나 전달할 정보에 대한 설명
-   schema.graphql에 사용자가 어떤 것을 할지에 대해 정의
    -   DB로 정보를 보내거나
    -   DB로 정보를 받거나

```graphql
type Query {
    name: String!
    <!-- 사용자에게 정보를 주는 것들을 넣음 -->
}

type Mutation   {
    <!-- 정보의 변형이 일어나는 것들을 넣음 -->
}
```

### Query

-   정보를 받을 때 사용

### Mutation

-   정보를 변형할 때 사용

## Resolver

```js
const resolvers = {
    Query: {
        name: () => "anna",
    },
};

export default resolvers;
```

-   query를 resolve한다는 의미
-   schema는 설명이고, resolver에서 query의 기능성을 프로그래밍
