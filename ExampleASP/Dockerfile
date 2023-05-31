FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
ENV ASPNETCORE_URLS http://+:5000

EXPOSE 5000

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY "./src/ExampleASP.csproj" .
RUN dotnet restore "./ExampleASP.csproj"

COPY ./src .
WORKDIR "/src/."
RUN dotnet build "ExampleASP.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ExampleASP.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ExampleASP.dll"]