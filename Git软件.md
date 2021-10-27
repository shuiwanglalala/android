# Git

git 本地创建分支并提交远程分支

```
git checkout -b xxx
git push origin test ：test
git push --set-upstream origin test
```

git删除本地分支、删除远程分支

```
git branch -d bug_xzx
git push origin --delete bug_xzx
```

git查看远程分支

```
git remote -v
```

git代理设置方法解决

```
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy https://127.0.0.1:1080
git config --global --unset http.proxy
git config --global --unset https.proxy
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```



[详细讲解Android Studio中使用Git——结合GitLab](https://www.jianshu.com/p/059ed1e01229)

https://github.com/github/gitignore

