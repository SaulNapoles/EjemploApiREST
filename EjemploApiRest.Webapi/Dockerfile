#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["EjemploApiRest.Webapi/EjemploApiRest.Webapi.csproj", "EjemploApiRest.Webapi/"]
RUN dotnet restore "EjemploApiRest.Webapi/EjemploApiRest.Webapi.csproj"
COPY . .
WORKDIR "/src/EjemploApiRest.Webapi"
RUN dotnet build "EjemploApiRest.Webapi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "EjemploApiRest.Webapi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "EjemploApiRest.Webapi.dll"]