FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 21153
EXPOSE 44333

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["TokenServiceApi/TokenServiceApi.csproj", "TokenServiceApi/"]
RUN dotnet restore "TokenServiceApi/TokenServiceApi.csproj"
COPY . .
WORKDIR "/src/TokenServiceApi"
RUN dotnet build "TokenServiceApi.csproj" -c Release -o /app


FROM build AS publish
RUN dotnet publish "TokenServiceApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TokenServiceApi.dll"]
