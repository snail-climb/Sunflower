# 🌻Sunflower

## 项目简介

> Sunflower 是一个专为团队项目部署打造的 GitLab CI/CD 流水线管理工具，旨在通过统一管控与高效整合，优化团队项目的构建、测试和部署流程。

## 目录结构

```
project/
├── eagle/
│   ├── ci.yaml          # 前端项目的 CI 配置
│   ├── cd.yaml          # 前端项目的 CD 配置
│   └── variables.yaml   # 前端项目 Eagle 的变量配置
└── dolphin/
    ├── ci.yaml          # 后端项目的 CI 配置
    ├── cd.yaml          # 后端项目的 CD 配置
    └── variables.yaml   # 后端项目 Dolphin 的变量配置
```

## 使用说明

1. **变量配置**

   在 `variables.yaml` 文件中配置项目所需的环境变量，包括 GitLab 信息、Docker 注册表信息、项目信息等。

2. **CI/CD 配置**

    - 在 `ci.yaml` 文件中配置项目构建阶段所需的流程，包括前后端打包、镜像构建和相关缓存优化。
    - 在 `cd.yaml` 文件中配置项目部署阶段所需的流程。

3. **触发流水线**

   在实际项目中编写 `.gitlab-ci.yaml` 文件，内容如下

   ```yaml
   include:
     - project: "ci-cd/pipeline-template"
       ref: main
       file:
         - "/project/dolphin/ci.yaml"
         - "/project/dolphin/cd.yaml"
   
   stages:
     - ci-build
     - ci-image-build
     - cd
   
   ci-build:
     stage: ci-build
     extends: [ .build ]
     allow_failure: false
   
   ci-image-build:
     stage: ci-image-build
     extends: [ .image-build ]
     allow_failure: false
   
   cd:
     stage: cd
     extends: [ .deploy ]
   ```

   通过 GitLab 界面或 API 触发 CI/CD 流水线。

## 贡献

欢迎任何形式的贡献！请提交问题或拉取请求，您的参与将使项目更加完善。

## 许可证

本项目采用 MIT 许可证，详细信息请参见 LICENSE 文件。

