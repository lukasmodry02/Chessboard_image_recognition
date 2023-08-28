FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["imige_recognition_load_and_display/imige_recognition_load_and_display.csproj", "imige_recognition_load_and_display/"]
RUN dotnet restore "imige_recognition_load_and_display/imige_recognition_load_and_display.csproj"
COPY . .
WORKDIR "/src/imige_recognition_load_and_display"
RUN dotnet build "imige_recognition_load_and_display.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "imige_recognition_load_and_display.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "imige_recognition_load_and_display.dll"]
