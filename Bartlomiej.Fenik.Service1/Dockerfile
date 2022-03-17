FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Bartlomiej.Fenik.Service1.csproj", "Bartlomiej.Fenik.Service1/"]
RUN dotnet restore "Bartlomiej.Fenik.Service1/Bartlomiej.Fenik.Service1.csproj"
COPY . Bartlomiej.Fenik.Service1/
WORKDIR "/src/Bartlomiej.Fenik.Service1"
RUN dotnet build "Bartlomiej.Fenik.Service1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Bartlomiej.Fenik.Service1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Bartlomiej.Fenik.Service1.dll"]