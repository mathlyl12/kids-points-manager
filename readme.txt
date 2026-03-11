================================================================================
                      儿童积分管理系统 - 项目说明
================================================================================

【项目名称】
儿童积分管理系统

【项目类型】
移动端 Web 应用（单页面 HTML）

【技术栈】
- 前端：原生 HTML + CSS + JavaScript
- 后端数据库：Supabase (PostgreSQL)
- CDN：jsdelivr (Supabase JS SDK)

【项目结构】
kids-points-deploy/
├── index.html          # 生产环境主文件
├── dev/
│   └── index.html     # 开发预览版本（修复 Android 兼容性问题）
├── preview/
│   └── index.html     # 旧预览版本（已弃用）
└── readme.txt         # 本说明文件

【功能列表】
1. 用户登录 - 使用昵称登录，数据存储在 localStorage
2. 添加小朋友 - 填写姓名和初始积分，支持自动生成6位关联码
3. 关联小朋友 - 通过6位关联码关联其他家长添加的小朋友
4. 积分管理 - 添加积分、扣除积分、积分兑换
5. 积分排名 - 显示所有小朋友的积分排名（含缓存优化）
6. 历史记录 - 查看每个小朋友的积分变动历史
7. 删除小朋友 - 删除小朋友及其相关记录

【数据库配置】
- Supabase URL: https://jjapnufndavlbtmqyufn.supabase.co
- Supabase Key: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImpqYXBudWZuZGF2bGJ0bXF5dWZuIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzI5NDk3OTMsImV4cCI6MjA4ODUyNTc5M30.yXciuHKpUe2PumtLCDGiCf-SepQqoHBTmPloXizwpbI
- 表名: kids

【数据库字段】
kids 表：
- id: 主键自增
- name: 小朋友姓名
- parent_id: 家长昵称（关联用）
- total_points: 积分余额
- kid_code: 6位关联码
- created_at: 创建时间
- history: 积分变动历史（JSON数组）

【GitHub 部署】
- 仓库地址: https://github.com/mathlyl12/kids-points-manager
- 生产版地址: https://mathlyl12.github.io/kids-points-manager/
- 预览版地址: https://mathlyl12.github.io/kids-points-manager/dev/
- 分支: main（同时包含生产版和预览版）

【开发注意事项】
1. Android 兼容性问题：登录后主界面可能不显示，需要在 showMain() 函数中添加：
   - loginSection.style.visibility = 'hidden';
   - mainSection.style.visibility = 'visible';
   - mainSection.style.opacity = '1';
   - mainSection.offsetHeight; // 触发重绘
   - document.body.style.background = 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)';

2. 积分排名缓存：30秒缓存，避免频繁查询数据库

3. 字段名注意：数据库使用 total_points（蛇形命名），代码中使用 kid.total_points

4. 生产发布流程：
   - 修改 dev/index.html 进行测试
   - 测试通过后，复制 dev/index.html 到 index.html
   - 同时提交两个文件到 main 分支

【常用命令】
# 推送修改
git add .
git commit -m "feat: 描述"
git push origin main

================================================================================
