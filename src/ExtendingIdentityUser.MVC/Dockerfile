#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["ExtendingIdentityUser.MVC/ExtendingIdentityUser.MVC.csproj", "ExtendingIdentityUser.MVC/"]
RUN dotnet restore "ExtendingIdentityUser.MVC/ExtendingIdentityUser.MVC.csproj"
COPY . .
WORKDIR "/src/ExtendingIdentityUser.MVC"
RUN dotnet build "ExtendingIdentityUser.MVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ExtendingIdentityUser.MVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ExtendingIdentityUser.MVC.dll"]
