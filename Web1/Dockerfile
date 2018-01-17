FROM  AS base
WORKDIR /app
EXPOSE 80

FROM  AS build
WORKDIR /src
COPY SF_Docker_SL_AspNet.sln ./
COPY Web1/Web1.csproj Web1/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/Web1
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Web1.dll"]
