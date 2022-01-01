## Lesson１. リゾルバを作成してみよう
### 前提 
index.jsをコピーして「lesson1.js」を作成  
packge.jsonのmainをsrc/lesson1.jsに変更

### ユーザー情報と型
```
let users = [
  {
    id: "1",
    name: "Mike Hattrup"
  },
  {
    id: "2",
    name: "Glen Plake"
  },
  {
    id: "3",
    name: "Scot Schmidt"
  }
];

const typeDefs = `
type Query {
  totalUsers: Int!
  allUsers: [User!]!
  user(id: ID!): User
}

type Mutation {
  createUser(name: String!): User!
}

type User {
  id: ID!
  name: String!
}
`
```
### やってみよう
1. ユーザー数を取得する、リゾルバとクエリを作成してみよう  
フィールド名:totalUsers

2. 全ユーザーを取得する、型、リゾルバ、クエリを作成してみよう  
ポイント...リゾルバの引数は1つ目が親フィールドリゾルバの戻り値、２つ目がGraphQL引数でオブジェクト型になっている。  
allUsers: (parent, args)

3. idからユーザー検索してみよう  
フィールド名:user

4. 新しいユーザーを追加しよう（終わった人用）  
フィールド名：createUser


```
// 4.ヒント
createUser(parent, args) {
  // 1.ユーザー情報を入れるオブジェクト
  // 2.usersに追加
  // 3.新しいユーザーを返す
}
```

## 答え
```
const resolvers = {
  Query: {
    totalUsers: () => users.length,
    allUsers: () => users,
    user: (parent, args) => users.find( user => user.id === args.id )
  },
  Mutation: {
    createUser(parent,args) {
      let _id = ++users.length
      let user = {
        id: _id,
        name: args.name
      }
      users.push(user)
      return user
    }
  },
  User: {
    id: (parent) => parent.id,
    name: (parent) => parent.name
  }
}
```

参考
https://www.apollographql.com/docs/apollo-server/data/resolvers/#defining-a-resolver
