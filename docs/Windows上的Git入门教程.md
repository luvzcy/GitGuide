

### Windows上的Git入门教程

本教程是window的Git教程，安装步骤暂时无，假设已经在计算机上安装了Git。

#### 用git创建一个本地仓库并将其push到远程仓库

1. 在本地创建一个 Git 仓库，可以使用以下命令：

```
git init
```

这个命令会在当前目录下创建一个空的 Git 仓库。

2. 在本地创建一些文件，可以使用文本编辑器或者其他工具，创建一些文件并保存到 Git 仓库中。
3. Git 2.30 版本及以后引入了一个新的安全特性，用于防止在不受信任的文件系统上执行 Git 操作，因为某些文件系统（如 Windows 上的 FAT32 或 NTFS）不记录文件的所有者信息。

   当 Git 检测到它在一个可能不安全的文件系统中操作时，它会显示这个警告并拒绝继续。在你的例子中，Git 检测到了你的存储库（`K:/learnsplace/my-study/spring-security-oauth-examples`）位于这样的文件系统中。

   为了解决这个问题，你可以按照错误提示中的建议，将你的存储库目录添加到 Git 的安全目录列表中。这可以通过运行以下命令来完成：

   ```
   git config --global --add safe.directory "本地仓库路径"
   ```

   这条命令告诉 Git 你的存储库目录是安全的，并允许你在该目录下执行 Git 操作。

   请注意，这个操作需要你有足够的权限来修改全局 Git 配置。如果你没有权限，你可能需要联系你的系统管理员或者使用 `--local` 选项来将目录添加到存储库特定的配置中，但这通常不是推荐的做法，因为它只会在当前存储库中生效。

   如果你确信你的文件系统是安全的，并且你信任你正在操作的存储库，那么添加这个例外通常是安全的。但是，如果你不确定，或者你在一个共享或不受信任的环境中工作，那么你应该谨慎行事，并考虑其他安全措施。
4. 将文件添加到 Git 仓库中，可以使用以下命令：

```
git add .
```

这个命令会将当前目录下所有的修改添加到 Git 仓库中。

5. 提交修改，可以使用以下命令：

```
git commit -m "提交信息"
```

这个命令会将修改提交到 Git 仓库中，并且添加提交信息。

6. 在 [GitHub](https://so.csdn.net/so/search?q=GitHub&spm=1001.2101.3001.7020) 或者其他远程仓库中创建一个仓库。

我打算将本次git学习做一个知识归档，到时候上传到git来学习，所有就以这个为例。

首先在 GitHub 的 `home` 目录找到 `Create a new repository` 。

选择一个名字，我这个仓库就叫 GitGuide 了。 

有 `Public` 和 `Private` 两个选择，如果不想给其他人访问到你的仓库，就选择 `Private` ，我这里就公开我的笔记了。

如果是直接在本地push，创建远程仓库时就不用创建 READEME file了，现在先什么也不管，直接点击 `Create repository` 创建。



创建完成后的远程参考就可以通过下面两个地址拉取仓库：

- https： https://github.com/luvzcy/GitGuide.git 

- ssh：git@github.com:luvzcy/GitGuide.git

一般用 https 的地址访问就行，因为使用 SSH 地址之前，你需要在对应的 GitHub 账户上设置 SSH 密钥，并在本地机器上生成并添加相应的公钥。这样，才可以通过 SSH 协议免密码地访问该 GitHub 仓库。

但我们是要push本地仓库，所以我们直接push就行。

7. 添加一个远程仓库的引用。

```
git remote add origin https://github.com/luvzcy/GitGuide.git
```

这个命令用于添加一个远程仓库的引用。在这个例子中，远程仓库的引用名是 `origin`（这是一个惯例，但你可以使用其他名称），而仓库的 URL 是 `git@github.com:luvzcy/GitGuide.git`，这是一个 SSH 格式的 URL，指向 GitHub 上的 `luvzcy/GitGuide` 仓库。

8. 重命名当前分支。

```
git branch -M main
```

这个命令用于重命名当前分支。`-M` 选项允许你在即使当前分支有上游（upstream）设置的情况下也强制重命名它。在这个例子中，命令假设当前分支名为 `master`（Git 早期版本的默认分支名），并将其重命名为 `main`（这是许多项目现在使用的默认分支名）。

如果你正在初始化一个新的仓库，并且从一开始就将默认分支设置为 `main`，那么这个命令可能不是必需的，除非你想确保分支名是 `main` 而不是从某个模板或早期版本的 Git 自动创建的 `master`。

9. 将本地 `main` 分支的更改推送到远程仓库的 `main` 分支。

```
git push -u origin main
```

`-u` 或 `--set-upstream` 选项将本地分支与远程分支关联起来，这样你就可以在后续的推送和拉取操作中使用简化的命令（例如，只需要 `git pull` 或 `git push` 而不是 `git pull origin main` 或 `git push origin main`）。

#### 结束