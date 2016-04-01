# WebHook-PHP
嗯~, 利用PHP实现 git WebHook 的自动化部署


---
>使用其它用户部分, 可略过...

```bash
groupadd www
useradd -g www -m -s /usr/sbin/nologin www #不让www用户直接登录
```

---

###Step 1
生成部署公钥

```bash
# 1.我们先查看, 要使用用户的家目录位置 比如 nginx
echo ~nginx
# 显示是在 /var/cache/nginx

# 2. 我们创建 .ssh目录, 用于存放部署公钥, 并设置权限
mkdir ~nginx/.ssh
# 查看所属用户组
groups nginx
# 显示是nginx

# 我们修改.ssh目录拥有者, 其它家目录和里面的文件不要管
chown nginx:nginx ~nginx/.ssh


# 3. 生成部署公钥, 并在 Git项目后台中添加
sudo -Hu nginx ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

cat ~nginx/.ssh/id_rsa.pub
```

###Step 2
写入钩子文件

```bash
mkdir /data/wwwroot/website.com/hook
chown -R nginx:nginx /data/wwwroot/website.com/hook
```

```bash
sudo -Hu nginx touch /data/wwwroot/website.com/hook/index.php

# 然后写入WebHook-PHP

```

###Step 3

修改配置文件
