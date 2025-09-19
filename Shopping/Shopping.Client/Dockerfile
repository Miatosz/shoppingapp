# Build stage
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /source

# Copy project file and restore
COPY Shopping.Client.csproj ./
RUN dotnet restore "Shopping.Client.csproj"

# Copy source and build/publish
COPY . .
RUN dotnet publish "Shopping.Client.csproj" -c Release -o /app /p:UseAppHost=false

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime
WORKDIR /app
EXPOSE 80
ENV ASPNETCORE_URLS=http://+:80

COPY --from=build /app .
ENTRYPOINT ["dotnet", "Shopping.Client.dll"]
#docker build --platform linux/amd64 -t miatosz/shoppingapp:latest .