#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Ti.Questions.API/Ti.Questions.API.csproj", "Ti.Questions.API/"]
RUN dotnet restore "Ti.Questions.API/Ti.Questions.API.csproj"
COPY . .
WORKDIR "/src/Ti.Questions.API"
RUN dotnet build "Ti.Questions.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Ti.Questions.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Ti.Questions.API.dll"]