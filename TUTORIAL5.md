# lesson5 機能追加
クエリを使用するためのステップは以下になります。
1. DBにテーブル追加(schema.prisma)
2. GraphQLのスキーマに型を追加(schema.graphql)
3. リゾルバ追加
4. index.jsでリゾルバを呼び出す
5. クエリ実行

### やってみよう
1. フィルタリング機能

2. ページネーション

3. 並べ替え

4. リンクの合計を取得する


`Query.js`
```
async function feed(parent, args, context, info) {
  const where = args.filter
    ? {
      OR: [
        { description: { contains: args.filter } },
        { url: { contains: args.filter } },
      ],
    }
    : {}

  const links = await context.prisma.link.findMany({
    where,
    skip: args.skip,
    take: args.take,
    orderBy: args.orderBy,
  })

  const count = await context.prisma.link.count({ where })

  return {
    links,
    count,
  }
}
```