# KAI SHING LUNG 网站部署指南

## 网站概述
- **品牌名称**: KAI SHING LUNG (启盛荣)
- **类型**: 企业展示+产品销售型官网
- **产品数量**: 49款礼服产品
- **技术栈**: HTML5 + Tailwind CSS + JavaScript

## 文件结构
```
启盛荣/
├── index.html          # 首页
├── products.html       # 产品中心
├── product.html        # 产品详情页（动态加载）
├── about.html          # 公司简介
├── contact.html        # 合作咨询
├── privacy.html        # 隐私政策
├── terms.html          # 使用条款
├── images/             # 产品图片（49款产品）
└── README_DEPLOY.md   # 本部署指南
```

## 功能特性
- ✅ 响应式设计（适配电脑端、移动端、平板）
- ✅ 深色/浅色模式切换（默认跟随系统设置）
- ✅ 产品筛选功能（按品类、价格）
- ✅ 产品排序功能
- ✅ 分页功能
- ✅ 联系表单（预留后台接口）
- ✅ 移动端汉堡菜单

## 部署方式

### 方式一：静态托管平台（推荐新手）

#### 1. Vercel 部署
```bash
# 安装 Vercel CLI
npm i -g vercel

# 进入项目目录
cd 启盛荣

# 部署
vercel

# 按提示操作即可
```

#### 2. Netlify 部署
1. 访问 https://www.netlify.com
2. 注册/登录账号
3. 点击 "Add new site" → "Deploy manually"
4. 将整个项目文件夹拖拽上传
5. 等待部署完成，自动分配域名

#### 3. GitHub Pages 部署
1. 创建 GitHub 仓库
2. 上传所有文件到仓库
3. 进入 Settings → Pages
4. Source 选择 "Deploy from a branch"
5. Branch 选择 "main"，文件夹选择 "/ (root)"
6. 保存后等待部署

### 方式二：云服务器部署（适合有技术基础）

#### 新星云部署步骤

1. **购买云服务器**
   - 访问新星云官网
   - 选择轻量应用服务器
   - 系统选择 Ubuntu 20.04 LTS 或 CentOS 8

2. **连接服务器**
   ```bash
   ssh root@你的服务器IP
   ```

3. **安装 Nginx**
   ```bash
   # Ubuntu
   apt update
   apt install nginx

   # CentOS
   yum install nginx
   ```

4. **配置 Nginx**
   ```bash
   # 编辑配置文件
   nano /etc/nginx/sites-available/default

   # 修改 root 路径
   root /var/www/html/启盛荣;

   # 保存并退出
   ```

5. **上传网站文件**
   ```bash
   # 创建目录
   mkdir -p /var/www/html/启盛荣

   # 使用 scp 上传（在本机执行）
   scp -r ./启盛荣/* root@你的服务器IP:/var/www/html/启盛荣/

   # 或使用 FileZilla 等 FTP 工具上传
   ```

6. **设置权限**
   ```bash
   chown -R www-data:www-data /var/www/html/启盛荣
   chmod -R 755 /var/www/html/启盛荣
   ```

7. **重启 Nginx**
   ```bash
   systemctl restart nginx
   ```

8. **开放防火墙端口**
   ```bash
   # Ubuntu (UFW)
   ufw allow 80
   ufw allow 443

   # 或在新星云控制台的安全组中开放 80 和 443 端口
   ```

9. **访问网站**
   - 输入你的服务器 IP 或域名即可访问

### 方式三：使用宝塔面板（最简单）

1. **安装宝塔面板**
   - 访问 https://www.bt.cn
   - 按文档安装宝塔面板

2. **添加网站**
   - 登录宝塔面板
   - 点击"网站" → "添加站点"
   - 填入域名或使用 IP
   - 根目录设置为网站文件夹

3. **上传文件**
   - 使用宝塔的文件管理器上传所有文件

4. **配置 SSL（可选）**
   - 点击"网站" → 对应网站 → "SSL"
   - 可选择 Let's Encrypt 免费证书

## 联系表单配置

当前联系表单已预留接口，需要配置后台才能接收邮件。有以下方案：

### 方案一：使用 Formspree（无需后端）
1. 注册 Formspree 账号 https://formspree.io
2. 创建新表单，获取表单 ID
3. 修改 contact.html 中的表单 action：
```html
<form action="https://formspree.io/f/你的表单ID" method="POST">
```

### 方案二：使用 Netlify Forms
如果部署在 Netlify，只需在表单标签添加：
```html
<form name="contact" netlify>
```

### 方案三：接入企业邮箱
联系苏先生配置企业邮箱接收表单数据。

## 注意事项

1. **图片路径**: 所有产品图片已正确引用在 images 文件夹中
2. **中文编码**: 文件已使用 UTF-8 编码，确保服务器也使用 UTF-8
3. **HTTPS**: 生产环境建议使用 HTTPS，可使用 Let's Encrypt 免费证书
4. **性能优化**: 图片已设置懒加载，首次加载速度快

## 联系方式
- **联系人**: 苏先生
- **电话**: +852 59735547
- **邮箱**: RodneyStevens8168@outlook.com

## 技术支持
如遇部署问题，可联系以上方式获取技术支持。
