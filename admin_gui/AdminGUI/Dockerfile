FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["AdminGUI/AdminGUI.csproj", "AdminGUI/"]
RUN dotnet restore "AdminGUI/AdminGUI.csproj"
COPY . .
WORKDIR "/src/AdminGUI"
RUN dotnet build "AdminGUI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AdminGUI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AdminGUI.dll"]