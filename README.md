# 克隆blog文件
1.1 克隆blog到本地路径，并保存为blog文件：
git clone https://github.com/sidney-neu/sidney-neu.github.io.git blog
# 安装npm和code
2.1 安装npm和node：
下载并安装 nvm：
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
2.2 代替重启 shell
\. "$HOME/.nvm/nvm.sh"
下载并安装 Node.js：
nvm install 20
2.3 验证验证 Node.js 版本：
node -v
验证 npm 版本：
npm -v
# 安装pandoc
 wget https://github.com/jgm/pandoc/releases/download/3.8.2/pandoc-3.8.2-1-amd64.deb
 sudo dpkg -i pandoc-3.8.2-1-amd64.deb
# 初始化并安装
hexo init      # 初始化
npm install    # 安装组件

hexo g   # 生成页面
hexo s   # 启动预览
