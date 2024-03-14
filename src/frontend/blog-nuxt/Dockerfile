# 使用Node.js 基础镜像
FROM node:18-alpine as base

WORKDIR /app
# node 运行端口
ENV PORT=5200
# 容器端口
EXPOSE 5200

FROM  base as build
WORKDIR /src
COPY . .
#设置镜像源
RUN yarn config set registry https://registry.npmmirror.com
RUN yarn && yarn run build

FROM publish as build
WORKDIR /publish
COPY --from=build /src/.output .output

FROM base as deploy
WORKDIR /app

COPY --from=publish  /publish/.output /app

CMD ["node","./server/index.mjs"]