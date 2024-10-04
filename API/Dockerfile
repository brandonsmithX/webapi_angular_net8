# Use the official .NET SDK image as the base image for building
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Set the working directory in the container
WORKDIR /app

# Copy the project file into the container
COPY ["API.csproj", "./"]

# Restore dependencies
RUN dotnet restore "API.csproj"

# Copy the rest of the application files
COPY . .

# Build and publish the application with detailed output
RUN dotnet build "API.csproj" -c Release -o /app/build --verbosity detailed

# Use the official ASP.NET runtime image for running the application
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final

WORKDIR /app

# Copy published output from build stage
COPY --from=build /app/build ./

# Specify the command to run the application
ENTRYPOINT ["dotnet", "API.dll"]