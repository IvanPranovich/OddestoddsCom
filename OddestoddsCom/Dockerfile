FROM ivanpranovitch/dotnetnodejs:2.2-aspnetcore-runtime-nodejs AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["OddestoddsCom/OddestoddsCom.csproj", "OddestoddsCom/"]
RUN dotnet restore "OddestoddsCom/OddestoddsCom.csproj"
COPY . .
WORKDIR "/src/OddestoddsCom"
RUN dotnet build "OddestoddsCom.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "OddestoddsCom.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "OddestoddsCom.dll"]