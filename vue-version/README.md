## 每次修改完vue项目后，请执行以下命令
## 测试（ctrl+c 结束）
npm run dev 
## 生产(一般是自动结束运行)
npm run build
## 把修改复制至主站
xcopy /E /I /Y dist\* ..\
## git命令 
git status 
git add .
git commit -m "feat:update"
## 如果提交错了，需要覆盖上一次提交记录，则用git commit --amend -m "feat:update"
## 查看提交记录(q退出)
git log
git push 