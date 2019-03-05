FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
RUN apt-get update -yq \
    && apt-get install curl gnupg -yq \
    && curl -sL https://deb.nodesource.com/setup_8.x | bash \
    && apt-get install nodejs -yq
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