FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["HelloWorld.csproj", "HelloWorld/"]	#相比原生命令去掉了HelloWorld/
RUN dotnet restore "HelloWorld/HelloWorld.csproj"
WORKDIR "/src/HelloWorld"	#相比原生命令二者调换了位置
COPY . .
RUN dotnet build "HelloWorld.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloWorld.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloWorld.dll"]