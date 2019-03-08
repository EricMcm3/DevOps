FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["DevOps.Api/DevOps.Api.csproj", "DevOps.Api/"]
RUN dotnet restore "DevOps.Api/DevOps.Api.csproj"
COPY . .
WORKDIR "/src/DevOps.Api"
RUN dotnet build "DevOps.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DevOps.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DevOps.Api.dll"]