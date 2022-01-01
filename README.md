# hackernews-graphql
デプロイ方法
GitHubアカウント登録

新しいRepositories作成

```
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:Nyamadamadamada/hackernews-graphql.git
git push -u origin main
```
参考
https://www.apollographql.com/docs/apollo-server/deployment/heroku/

Herokuアカウント登録  
[https://dashboard.heroku.com/login](https://dashboard.heroku.com/login)

Resouce/Add-onsから「Find more add-ons」からHeroku Postgresを選択

```
// プリズマの初期化
npx prisma init    
// schema.prisma修正後
npx prisma db push                     
```


```
heroku buildpacks
heroku buildpacks:set heroku/nodejs
git push heroku main
```

ポートが埋まっていた時
```
lsof -i :4000
kill -9 <PID>
```