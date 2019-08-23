FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["CharacteristicsManagement/CharacteristicsManagement.csproj", "CharacteristicsManagement/"]
RUN dotnet restore "CharacteristicsManagement/CharacteristicsManagement.csproj"
COPY . .
WORKDIR "/src/CharacteristicsManagement"
RUN dotnet build "CharacteristicsManagement.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CharacteristicsManagement.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CharacteristicsManagement.dll"]