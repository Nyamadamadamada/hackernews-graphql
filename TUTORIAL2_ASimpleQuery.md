## lession2 CRUD機能の実装

### 型
```
type Query {
  # Fetch a single link by its `id`
  link(id: ID!): Link
}

type Mutation {
  # Update a link（updateLink）

  # Delete a link（deleteLink）
}
```


### やってみよう
1. Linkを更新してみよう  
updateLink
2. Linkを削除してみよう
戻り値は削除に成功したかどうかのメッセージを返す  
例）「"link-0を削除しました"」「”link-0は存在しません”」
deleteLink


## 答え




```
// schema.graphql
type Mutation {
  post(url: String!, description: String!): Link!
  
  # Update a link
  updateLink(id: ID!, url: String, description: String): Link

  # Delete a link
  deleteLink(id: ID!): String
}
// index.js
updateLink: (parent, args) => {
  let updateLink = links.find( link => link.id === args.id)
  if (updateLink.url) {
    updateLink.url = args.url
  }
  if (args.description) {
    updateLink.description = args.description
  }
  return updateLink
},
deleteLink: (parent, args) => {
  const oldLinksCount = links.length
  links = links.filter( link => {
    return link.id !== args.id
  })
  const newLinksCount = links.length
  if (oldLinksCount === newLinksCount) {
    return `${args.id}の削除に失敗しました ` 
  }
  return `${args.id}を削除しました ` 
}
```