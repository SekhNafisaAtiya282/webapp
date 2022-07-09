#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["WebApplication2prac/WebApplication2prac.csproj", "WebApplication2prac/"]
RUN dotnet restore "WebApplication2prac/WebApplication2prac.csproj"
COPY . .
WORKDIR "/src/WebApplication2prac"
RUN dotnet build "WebApplication2prac.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApplication2prac.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication2prac.dll"]