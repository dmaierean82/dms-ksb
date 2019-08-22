FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["VariantCharacteristicsManagement/VariantCharacteristicsManagement.csproj", "VariantCharacteristicsManagement/"]
RUN dotnet restore "VariantCharacteristicsManagement/VariantCharacteristicsManagement.csproj"
COPY . .
WORKDIR "/src/VariantCharacteristicsManagement"
RUN dotnet build "VariantCharacteristicsManagement.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "VariantCharacteristicsManagement.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "VariantCharacteristicsManagement.dll"]