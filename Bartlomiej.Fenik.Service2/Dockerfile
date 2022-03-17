FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Bartlomiej.Fenik.Service2.csproj", "Bartlomiej.Fenik.Service2/"]
RUN dotnet restore "Bartlomiej.Fenik.Service2/Bartlomiej.Fenik.Service2.csproj"
COPY . Bartlomiej.Fenik.Service2/
WORKDIR "/src/Bartlomiej.Fenik.Service2"
RUN dotnet build "Bartlomiej.Fenik.Service2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Bartlomiej.Fenik.Service2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Bartlomiej.Fenik.Service2.dll"]