FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["MySecondWebApp/MySecondWebApp.csproj", "MySecondWebApp/"]
RUN dotnet restore "MySecondWebApp/MySecondWebApp.csproj"
COPY . .
WORKDIR "/src/MySecondWebApp"
RUN dotnet build "MySecondWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MySecondWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MySecondWebApp.dll"]

# Start the dotnet application on port 5000.
#CMD ["dotnet", "run", "--server.urls", "http://localhost:5000"]