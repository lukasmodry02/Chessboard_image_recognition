FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["image_to_chess_notation.csproj", "./"]
RUN dotnet restore "image_to_chess_notation.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "image_to_chess_notation.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "image_to_chess_notation.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "image_to_chess_notation.dll"]
