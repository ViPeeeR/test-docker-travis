FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 57712
EXPOSE 44399

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY DockerTest/DockerTest.csproj DockerTest/
RUN dotnet restore DockerTest/DockerTest.csproj
COPY . .
WORKDIR /src/DockerTest
RUN dotnet build DockerTest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerTest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerTest.dll"]
