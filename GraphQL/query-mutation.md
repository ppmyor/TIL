## Query

-   DB의 정보를 볼 때 사용

```graphql
type Query {
    movies: [Movie]!
    movie(id: Int!): Movie
}
```

-   schema에는 type Query를 선언한 후 argument의 type과 return 값 등의 정보를 넘겨줌

```js
const resolver = {
    Query: {
        movies: () => getMovies(),
        movie: (_, { id }) => getById(id),
    },
};
```

-   resolver에는 resolver 내부에 Query를 선언한 후 정보를 가져올 관련 함수에 대해 기재

## Mutation

-   DB의 정보를 변형할 때 사용
    -   DB에 정보를 추가하거나, 삭제 하는 등의 작업

```graphql
type Mutation {
    addMovie(name: String!, score: Int!): Movie!
    deleteMovie(id: Int!): Boolean!
}
```

-   schema에는 type Mutataion을 선언한 후 argument의 type과 return 값 등의 정보를 넘겨줌

```js
const resolver = {
    Mutation: {
        addMovie: (_, { name, score }) => addMovie(name, score),
        deleteMovie: (_, { id }) => deleteMovie(id),
    },
};
```

-   resolver에는 resolver 내부에 Mutation을 선언한 후 정보 변형과 관련 함수에 관한 것들을 기재
