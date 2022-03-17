FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Bartlomiej.Fenik.Service3.csproj", "Bartlomiej.Fenik.Service3/"]
RUN dotnet restore "Bartlomiej.Fenik.Service3/Bartlomiej.Fenik.Service3.csproj"
COPY . Bartlomiej.Fenik.Service3/
WORKDIR "/src/Bartlomiej.Fenik.Service3"
RUN dotnet build "Bartlomiej.Fenik.Service3.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Bartlomiej.Fenik.Service3.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Bartlomiej.Fenik.Service3.dll"]