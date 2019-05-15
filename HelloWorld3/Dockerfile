FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["HelloWorld3/HelloWorld3.csproj", "HelloWorld3/"]
RUN dotnet restore "HelloWorld3/HelloWorld3.csproj"
COPY . .
WORKDIR "/src/HelloWorld3"
RUN dotnet build "HelloWorld3.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloWorld3.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloWorld3.dll"]