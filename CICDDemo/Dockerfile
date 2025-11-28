# 基础镜像：用官方.NET 8 SDK（构建用）
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# 复制项目文件，还原依赖
COPY *.csproj ./
RUN dotnet restore

# 复制所有代码，构建发布
COPY . ./
RUN dotnet publish -c Release -o out

# 运行镜像：用轻量的.NET 8运行时（减少镜像体积）
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/out .

# 启动服务
ENTRYPOINT ["dotnet", "CICDDemo.dll"]