FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["VariantManagement/VariantManagement.csproj", "VariantManagement/"]
RUN dotnet restore "VariantManagement/VariantManagement.csproj"
COPY . .
WORKDIR "/src/VariantManagement"
RUN dotnet build "VariantManagement.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "VariantManagement.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "VariantManagement.dll"]