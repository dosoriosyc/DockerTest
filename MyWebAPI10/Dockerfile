FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 54486
EXPOSE 44359

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["MyWebAPI10/MyWebAPI10.csproj", "MyWebAPI10/"]
RUN dotnet restore "MyWebAPI10/MyWebAPI10.csproj"
COPY . .
WORKDIR "/src/MyWebAPI10"
RUN dotnet build "MyWebAPI10.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MyWebAPI10.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MyWebAPI10.dll"]