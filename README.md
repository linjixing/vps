
# 参考
https://www.youtube.com/watch?v=WPaKP1l0FdE

# 创建方法

## 方法一: 自建仓库

### 1. 新建仓库
- Repository name: **vps**
- Add README: **on**
- Create repository

### 2. 创建codespace
- 进入codespace首页
- https://github.com/codespaces
- 点击New codespace
- 选择新建的仓库: **vps**
- Create codespace on main

### 3. 修改codespace配置
- 进入codespace首页
- 点击对应codespace后面的 ==...==
- 点击Change machine type
- 修改为4-core
- Update codespace

### 4. 新建项目

```
vi docker-compose.yaml
```

```
services:
  wordpress:
    image: wordpress:latest # 使用官方 WordPress Docker 镜像
    ports:
      - "80:80" # 将容器的 80 端口映射到 Codespace 的 80 端口
    environment:
      WORDPRESS_DB_HOST: db:3306 # 数据库主机名和端口
      WORDPRESS_DB_USER: wordpress # 数据库用户名
      WORDPRESS_DB_PASSWORD: wordpress # 数据库密码
      WORDPRESS_DB_NAME: wordpress # 数据库名称
    volumes:
      - ./html:/var/www/html # 将本地 html 目录映射到容器的 Web 根目录，放你的 WordPress 代码
    depends_on:
      - db

  db:
    image: mysql:8.0 # 使用 MySQL 8.0 镜像
    environment:
      MYSQL_ROOT_PASSWORD: root # MySQL root 用户密码
      MYSQL_DATABASE: wordpress # 创建的数据库名称
      MYSQL_USER: wordpress # 创建的数据库用户
      MYSQL_PASSWORD: wordpress # 创建的数据库密码
    volumes:
      - db_data:/var/lib/mysql # 持久化数据库数据

volumes:
  db_data: # 定义一个数据卷来持久化数据库数据

```

### 5. 运行项目

```
docker-compose up -d
```

https://glowing-tribble-q696q967j6w2xg7g-80.app.github.dev/

## 方法二: 从template创建

- 进入模板首页

- https://github.com/codespaces/templates

- 选择一个模板点击: Use this template
