FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 54596
EXPOSE 44346

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY SCVDotNet/SCVDotNet.csproj SCVDotNet/
RUN dotnet restore SCVDotNet/SCVDotNet.csproj
COPY . .
WORKDIR /src/SCVDotNet
RUN dotnet build SCVDotNet.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish SCVDotNet.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SCVDotNet.dll"]
