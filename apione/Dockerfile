FROM microsoft/aspnetcore-build:2.0 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/aspnetcore:2.0.9
WORKDIR /app
COPY --from=build-env /app/out .
RUN mkdir -p /app/etc/keys
EXPOSE 80
ENTRYPOINT ["dotnet", "apione.dll"]