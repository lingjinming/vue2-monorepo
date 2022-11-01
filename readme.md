# Monorepo

[Better practice npm Package Design in Monorepo](https://www.rustc.cloud/monorepo-pkg) with [pnpm](https://pnpm.io/) and [turborepo](https://turborepo.org/), deploying into [Vercel](https://vercel.com/).

## Quick Start

```bash
$ npm i -g pnpm
$ pnpm -v # should >= 6.20.0 
# Install vuecli # should >= 4.5.10
$ pnpm i -g vue-cli
```

```bash
$ pnpm install
```

### 分别启动mis和gis项目

```bash
# Start mis、gis App
$ pnpm serve:mis
$ pnpm serve:gis
```

### 项目安装各自的依赖可以利用 pnpm -F命令

```bash
$ pnpm i -F mis echarts
```
