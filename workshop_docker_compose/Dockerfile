FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY [".", "."]
RUN dotnet restore "workshop_docker_compose.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "workshop_docker_compose.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "workshop_docker_compose.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "workshop_docker_compose.dll"]
