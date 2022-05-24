#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["webAppDemo/webAppDemo.csproj", "webAppDemo/"]
RUN dotnet restore "webAppDemo/webAppDemo.csproj"
COPY . .
WORKDIR "/src/webAppDemo"
RUN dotnet build "webAppDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "webAppDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "webAppDemo.dll"]