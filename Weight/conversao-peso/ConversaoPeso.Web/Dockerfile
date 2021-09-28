FROM .NET AS base
WORKDIR /app
EXPOSE 80

FROM .NETCoreSDK AS build
WORKDIR /src 
COPY ["ConversaoPeso.Web/ConversaoPeso.Web.csproj", "ConversaoPesoDocker/"]
RUN dotnet restore "ConversaoPeso.Web/ConversaoPeso.Web.csproj" 
COPY . .  
WORKDIR "/src/dockerdemowebapp"  
RUN dotnet build "dockerdemowebapp.csproj"

FROM build AS publish  
RUN dotnet publish "ConversaoPeso.Web.csproj" 

FROM base AS final  
WORKDIR /app  
COPY --from=publish /app .  
ENTRYPOINT ["dotnet", "conversaodocker.dll"]